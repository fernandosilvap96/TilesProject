<template>
  <div class='page'>
    <div class='content'>
      <div class='header'>
        <img src='~/assets/logo.png' alt=''>
        <a href='/'>Home</a>
        <a href='/home'>How it works</a>
        <a href='/home'>FAQ</a>
        <a href='/home'>Contacts</a>
      </div>
      <div class='about-block'>
        <popup v-if='walletPopup'>
          <wallet @setWalletKey='setWalletKey' @walletClose='walletClose' />
        </popup>
        <popup v-if='loading'>
          <wait-transaction :transactionInfo='transactionInfo' />
        </popup>
        <popup v-if='successPopup'>
          <transaction-success :transactionInfo='transactionInfo' />
        </popup>
        <div class='mobile-history'>
          <h1 class='history-title mobile-history'>CUSTOMIZE YOUR TILE</h1>
          <div class='upload-buttons mobile-history'>
            <div class='upload-buttons-item'>
              <label>
                <img src='~/assets/upload-image.svg' alt=''>
                <p>image</p>
                <input
                  class='input-upload'
                  ref="upload"
                  type="file"
                  name="file-upload"
                  multiple=""
                  accept="image/jpeg, image/png"
                  @change="inputFile">
              </label>
            </div>
            <div class='upload-buttons-item'>
              <label>
                <img src='~/assets/video.svg' alt=''>
                <p>video</p>
                <input
                  class='input-upload'
                  ref="upload"
                  type="file"
                  name="file-upload"
                  multiple=""
                  accept="video/*"
                  @change="inputFileVideo">
              </label>

            </div>
          </div>
        </div>
        <component
          :is='editBlockComponent'
          :src='src'
          :inlineResult='inlineResult'
          :uploadElement='uploadElement'
          @handleInlineProcess='handleInlineProcess'
        />
        <div class='about-block__description'>
          <div class='history'>
            <h1 class='history-title desktop'>CUSTOMIZE YOUR TILE</h1>
            <div class='upload-buttons desktop'>
              <div class='upload-buttons-item'>
              <label>
                  <img src='~/assets/upload-image.svg' alt=''>
                  <p>image</p>
                <input
                  class='input-upload'
                  ref="upload"
                  type="file"
                  name="file-upload"
                  multiple=""
                  accept="image/jpeg, image/png"
                  @change="inputFile">
              </label>
              </div>
              <div class='upload-buttons-item'>
                <label>
                  <img src='~/assets/video.svg' alt=''>
                  <p>video</p>
                  <input
                    class='input-upload'
                    ref="upload"
                    type="file"
                    name="file-upload"
                    multiple=""
                    accept="video/*"
                    @change="inputFileVideo">
                </label>

              </div>
            </div>

            <label class='element-link-label'>
              <small>link</small>
              <input type='text'>
            </label>

            <div v-if='errorText' class='save-buttons error-text'>
              <p>{{errorText}}</p>
            </div>
            <div v-if='loading === false' class='save-buttons'>
              <button @click='uploadToArweave()' class='save-buttons__save'>Save and close</button>
              <button class='save-buttons__cancel'>Cancel</button>
            </div>
          </div>
        </div>
      </div>

    </div>
    <div class='footer'>
      <p>© 2021 10 Tiles LTD.</p>
    </div>
  </div>
</template>

<script>



// Import the editor default configuration
import { getEditorDefaults } from 'pintura';

import arweave from '../service/arweave'
import EditIdle from '../components/editIdle'
import Popup from '../components/popup'
import Wallet from '../components/wallet'
import WaitTransaction from '../components/waitTransaction'
import TransactionSuccess from '../components/transactionSuccess'
// import { ArweaveSigner, createData } from "arbundles";

const states = {
  idle: EditIdle
}
let getStatus
export default {
  name: 'editor',
  components: {
    TransactionSuccess,
    WaitTransaction,
    Wallet,
    Popup,
    EditIdle
  },
  data() {
    return {
      editState: 'idle',
      // Pass the editor default configuration options
      editorDefaults: getEditorDefaults(),
      inlineResult: undefined,
      // The source image to load
      src: undefined,
      // This will set a square crop aspect ratio
      uploadElement: 'image',
      errorText: '',
      walletKey: undefined,
      transactionInfo: {},

      successPopup: false,
      waitLoading: false,
      loading: false,
      walletPopup: false,
    };
  },
  computed: {
    editBlockComponent() {
      return states[this.editState]
    }
  },
  methods: {
    handleInlineProcess(event){
      this.inlineResult = URL.createObjectURL(event.dest);
    },
    inputFile(event){
      if (!event.target.files.length) {
        return
      }
      this.src = event.target.files[0]
      this.uploadElement = 'image'
    },
    inputFileVideo(event){
      console.log(event)
      if (!event.target.files.length) {
        return
      }
      this.src = event.target.files[0]
      this.inlineResult = URL.createObjectURL(this.src);
      this.uploadElement = 'video'
    },
    async uploadToArweave(){
      this.errorText = ''
      console.log(this.src)
      if (!this.src) {
        this.errorText = 'input image or video'
        return false
      }

      try{
        this.walletPopup = true
      }catch (err) {
        this.walletPopup = false
        this.errorText = 'transaction error. try again'
      }


    },
    async setWalletKey(key) {
      this.walletKey = key
      this.walletPopup = false
      try {
        this.loading = true
        const type = this.src.type
        const imageDataUri = await this.toBase64(this.src)
        const imageBuffer = Buffer.from(imageDataUri.split(",")[1], "base64");
        const transaction = await arweave.createTransaction(
          {
            data: imageBuffer
          },
          key
        );
        transaction.addTag('Content-Type', type);
        await arweave.transactions.sign(transaction, key);
        await arweave.transactions.post(transaction);
        // console.log("post response", postResponse);
        // console.log('getStatus',await arweave.transactions.getStatus(transaction.id))
        this.transactionInfo = {
          address: await arweave.wallets.jwkToAddress(key),
          transactionId: transaction.id
        }
        getStatus = setInterval( () => this.getTransactionStatus(), 60000)
      }catch (err) {

      }

    },
    async getTransactionStatus(){
      let status = await arweave.transactions.getStatus(this.transactionInfo.transactionId)
      console.log(status)
      if (status.status !== 202 ) {
        clearInterval(getStatus)
      }
      if (status.status === 200) {
        this.loading = false
        this.successPopup = true
      }
      return status
    },
    toBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => resolve(reader.result);
        reader.onerror = error => reject(error);
      })
    },
    walletClose(){
      this.walletPopup = false
    }
  }
}
</script>

<style lang='scss'>
@import '../node_modules/pintura/pintura.css';

.page{
  min-height: 100vh;
  height: 100%;
  background: rgb(9,9,126);
  background:linear-gradient(38deg, #09097e 24%, #510074 100%);
  position: relative;
  display: grid;
  grid-template-rows: 1fr auto;
  padding: 0 16px;

  .content {
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;
    .about-block {
      position: relative;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 120px;
      margin-top: 60px;
      &__block {
        min-height: 460px;
        border-radius: 30px;
        border: 2px dashed rgba(255,255,255, 0.3);
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        .block-elements{
        }
        &--video {
          border: none;
        }
        @media screen and (max-width: 768px) {
          min-height: 300px;
        }
      }
      &__description{
        .des-buttons {
          display: grid;
          grid-template-columns: auto 1fr 1fr;
          gap: 24px;
          margin-bottom: 72px;
          .price {
            .block-price {
              color: #00fc7b;
              line-height: 1.5;
              display: flex;
              align-items: center;
              font-size: 24px;
              &:after {
                content: url("~/assets/eth.png");
                margin-left: 4px;
              }
            }
            .block-price-dollar {
              font-size: 14px;
            }
          }
          .buy-now {
            background: #090069;
            padding: 18px;
            border-radius: 12px;
            text-align: center;
          }
          .place-bid {
            background: #ff2dac;
            padding: 18px;
            border-radius: 12px;
            text-align: center;
          }
        }

      }
      @media screen and (max-width: 1024px) {
        gap: 50px;
      }
      @media screen and (max-width: 768px) {
        grid-template-columns: 1fr;
      }
    }
    .input-image {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100%;

      img {
        width: 40%;
        opacity: 0;
      }
      input{
        width: 0;
        height: 0;
      }
      &:hover {
        cursor: pointer;
        img {
          transition: .4s;
          opacity: .6;
        }
      }
    }
  }
  @media screen and (max-width: 768px) {
    background:linear-gradient(38deg, #09097e 80%, #af00ff 100%);
    .page-background-text {
      display: none;
    }
    .content {
      background-size: 300px;
      background-position: right 100px;
      .header {
        a {
          font-size: 14px;
        }
      }
    }

  }
}
.input-upload {
  width: 0;
  height: 0;
  position: absolute;
}
.save-buttons {
  display: grid;
  grid-template-columns: auto auto;
  gap: 24px;
  margin-top: 50px;
  &__save{
    background: #090069;
    padding: 18px;
    border-radius: 12px;
    text-align: center;
    color: inherit;
    font-family: inherit;
    font-size: 14px;
    font-weight: inherit;
    outline: none;
    border: none;
    &:hover {
      cursor: pointer;
    }
  }
  &__cancel {
    background: #ff2dac;
    padding: 18px;
    border-radius: 12px;
    text-align: center;
    color: inherit;
    font-family: inherit;
    font-size: 14px;
    font-weight: inherit;
    outline: none;
    border: none;
    &:hover {
      cursor: pointer;
    }
  }
}
.history {
  .element-link-label {
    display: flex;
    flex-direction: column;
    small {
      font-size: 12px;
    }
    input {
      background-color: rgba(0,0,0,0);
      outline: none;border: none;
      font-size: 18px;
      color: white;
      padding: 8px 0px;
      border-bottom: 2px solid white;
    }
  }
}

.history-title {
  font-size: 32px;
  color: white;
  font-family: 'Bungee', cursive;
  @media screen and (max-width: 768px) {
  }
}
.upload-buttons {
  display: grid;
  grid-template-columns: 80px 80px;
  grid-template-rows: 90px;
  gap: 24px;
  margin-top: 30px;
  margin-bottom: 70px;
  .upload-buttons-item {
    background-color: white;
    border-radius: 12px;
    display: flex;
    flex-direction: column;
    align-items: center;
    label {
      padding: 12px;
    }
    img {
      width: 45px;
      height: 45px;
    }
    p {
      color: #09097e;
    }
    &:hover {
      cursor: pointer;
      -webkit-box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
      -moz-box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
      box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
      background: white;
      transition: 0.3s;
    }
  }
  @media screen and (max-width: 768px) {
    margin-top: 30px;
    margin-bottom: 0;
  }
}

video {
  width: 100%;
}
input[type="file"] {
  width: 0.1px;
  height: 0.1px;
  opacity: 0;
  overflow: hidden;
  position: absolute;
  z-index: -1;
}

.error-text {
  p {
    color: orangered;
  }
}
.mobile-history {
  @media screen and (min-width: 768px) {
    display: none;
  }
}
.desktop {
  @media screen and (max-width: 768px) {
    display: none !important;
  }
}
</style>
