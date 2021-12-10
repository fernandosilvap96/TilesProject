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
        <div class='about-block__block'>
          <div class='block-elements'>
            <h1 class='element-title'>TILES <br>#{{$route.params.id}}</h1>
            <p class='element-des'>Participate in the auction for each tile. The buyer gets the opportunity to leave a message.</p>
            <p class='element-des-2'>The tiles can be resold.</p>
          </div>
        </div>
        <div class='about-block__description'>
          <h1 class='about-block-title'>TILE #{{$route.params.id}}</h1>
          <div class='des-buttons'>
            <div class='price'>
              <p class='block-price'>0.1</p>
              <p class='block-price-dollar'>$416</p>
            </div>
            <nuxt-link to='#' class='buy-now buttons-mobile'>Buy now!</nuxt-link>
            <nuxt-link to='#' class='place-bid buttons-mobile'>Place a bid</nuxt-link>
          </div>
          <div class='history'>

            <div class='history-item'>
              <p>Owner: <span>1234512345</span></p>
              <p>Contract Address: <span>1234512345</span></p>
              <p>Metadata on Arweave: <span>1234512345</span></p>
              <p>Token ID: <span>1234512345</span></p>
            </div>
            <h1 class='history-title'>HISTORY</h1>
            <div class='history-blocks'>
              <div v-for='i in 4' class='history-blocks__block'>
                <img class='history-blocks__block-image' src='~/assets/user-icon.svg' alt=''>
                <div class='history-blocks__block-content'>
                  <p class='history-blocks__block-title'>Listed for <span>0.1 <img src='~/assets/eth.png' alt=''></span></p>
                  <p class='history-blocks__block-des'>by a 12341234 1 hour ago</p>
                </div>
              </div>
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
export default {
  name: 'nftAbout'
}
</script>

<style lang='scss'>
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
    //width: 100%;
    margin: 0 auto;

    .about-block {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 120px;
      margin-top: 60px;
      .about-block-title {
        font-size: 54px;
        line-height: 50px;
        color: #00fc7b;
        font-weight: 400;
        font-family: 'Bungee', cursive;

        margin-bottom: 14px;
      }
      &__block {
        min-height: 460px;
        border-radius: 30px;
        border: 2px dashed rgba(255,255,255, 0.3);
        padding: 40px 30px;
        background-image: url("~/assets/man.png");
        background-repeat: no-repeat;
        background-position: 50px 50px;
        background-size: 200px;
        .block-elements{
          .element-title {
            font-size: 75px;
            line-height: 66px;
            color: #00fc7b;
            font-weight: 400;
            font-family: 'Bungee', cursive;
            margin-top: 200px;
            margin-bottom: 40px;
          }
          .element-des {
            font-size: 14px;
            line-height: 24px;
            margin-bottom: 18px;
          }
          .element-des-2 {
            font-size: 14px;
            line-height: 24px;
            color: #108d7f;
          }
        }
      }
      &__description{
        .des-buttons {
          display: grid;
          grid-template-columns: auto 1fr 1fr;
          gap: 24px;
          margin-bottom: 48px;
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
        .history {
          .history-title {
            font-size: 32px;
            font-weight: bold;
            font-family: "Bungee", cursive;
            color: white;
          }
          .history-item {
            margin: 24px 0;
            p {
              margin-bottom: 10px;
              font-size: 14px;
              span {
                color: #00fc7b;
              }
            }
          }
          .history-blocks {
            margin-top: 12px;
            &__block {
              margin-bottom: 12px;
              display: grid;
              grid-template-columns: auto 1fr;
              gap: 16px;
              &-image {
                width: 40px;
                height: auto;

              }
              &-content {
                display: flex;
                flex-direction: column;
                justify-content: space-around;
              }
              &-title {
                img {
                  width: 10px;
                }
              }
              &-des {
                font-size: 12px;
                font-weight: lighter;
              }
            }
          }
        }
      }
      @media screen and (max-width: 768px) {
        grid-template-columns: 1fr;
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
.buttons-mobile {
  @media screen and (max-width: 768px) {
    font-size: 14px;
    padding: 6px !important;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
