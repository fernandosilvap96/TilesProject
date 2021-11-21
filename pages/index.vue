<template>
  <div class='page-about'>
    <h1 class='page-background-text'>NFT TILES</h1>
    <div class='content'>
      <div class='header'>
        <img src='~/assets/logo.png' alt=''>
        <a href='/'>Home</a>
        <a href='/home'>How it works</a>
        <a href='/home'>FAQ</a>
        <a href='/home'>Contacts</a>
      </div>
      <div class='main'>
        <h1 class='title'><span>10</span> UNIQUE <br> NFT TILES</h1>
        <p class='title-description'>Participate in the auction for each tile.</p>
        <p class='title-description'>The buyer gets the opportunity to leave a message.</p>
        <p class='title-description title-description-unique'>The tiles can be resold.</p>
      </div>
      <div class='blocks'>
        <div class='none'></div>

        <nuxt-link v-for='item in 10' :to='`/nft/${item}`' :key='item' class='block'>
          <div>
            <p class='block-price'>0.1</p>
            <p class='block-price-dollar'>$416</p>
          </div>
          <div  class='buy-now-link'>Buy now!</div>
        </nuxt-link>

        <div class='none'></div>

      </div>
    </div>
    <div class='footer'>
      <p>© 2021 Reat Media Limited. All right registered</p>
    </div>
  </div>
</template>


<script>
export default {}
</script>
<style lang='scss'>
.page-about{
  min-height: 100vh;
  height: 100%;
  background: rgb(9,9,126);
  background:linear-gradient(38deg, #09097e 24%, #510074 100%);
  position: relative;
  display: grid;
  grid-template-rows: 1fr auto;
  padding: 0 16px;

  .page-background-text {
    position: absolute;
    top: 262px;
    left: 0;
    right: 0;
    font-size: 320px;
    white-space: nowrap;
    font-family: 'Bungee', cursive;
    color: rgba(255,255,255, 0.2);
    overflow: hidden;
  }
  .content {
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;

    background-image: url("~/assets/man.png");
    background-repeat: no-repeat;
    background-position: right 50px;
    background-size: 600px;


    .main {
      .title {
        font-size: 75px;
        line-height: 66px;
        color: #00fc7b;
        font-weight: 400;
        font-family: 'Bungee', cursive;
        margin-top: 200px;
        margin-bottom: 40px;
        span {
          color: #00ffff
        }
      }
      .title-description {
        margin-bottom: 16px;
        font-size: 16px;
        line-height: 24px;
        //color: #ffffff;
        font-weight: 600;
      }
      .title-description-unique {
        margin-top: 30px;
        color: #00fc7b;
      }
      margin-bottom: 240px;
    }
    .blocks {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr 1fr;
      gap: 24px;
      padding-bottom: 100px;

      .block {
        padding: 20px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        border: 2px dashed rgba(255,255,255, 0.5);
        min-height: 282px;
        border-radius: 30px;
        transition: 0.3s;
        .buy-now-link {
          background: #090069;
          padding: 18px;
          border-radius: 12px;
          text-align: center;
        }
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
        &:hover {
          cursor: pointer;
          -webkit-box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
          -moz-box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
          box-shadow: 1px 14px 62px 11px rgba(0, 252, 123, 1);
          background: white;
          transition: 0.3s;
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
      .main {
        margin-bottom: 50px;
        .title {
          font-size: 60px;
        }
      }
      .blocks {
        grid-template-columns: 1fr 1fr;
        .none {
          display: none;
        }
        .block {
          min-height: 180px;
        }
      }
    }

  }
}
</style>
