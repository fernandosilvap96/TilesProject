<template>
  <div class="page-about">
    <h1 class="page-background-text">NFT TILES</h1>
    <div class="content">
      <div class="header">
        <img src="~/assets/logo.png" alt="" />
        <a href="/">Home</a>
        <a href="/home">How it works</a>
        <a href="/home">FAQ</a>
        <a href="/home">Contacts</a>
      </div>
      <div class="main">
        <h3>Account: {{ account }}</h3>
        Wallet:
        <a
          v-for="token in tokenIds"
          :href="base + token"
          :key="token"
          class="title-description title-description-unique"
          target="_blank"
        >
          TOKEN {{ token }} ,
        </a>
        <h1 class="title">
          <span>10</span> UNIQUE <br />
          NFT TILES
        </h1>
        <p class="title-description">
          Participate in the auction for each tile.
        </p>
        <p class="title-description">
          The buyer gets the opportunity to leave a message.
        </p>
        <p class="title-description title-description-unique">
          The tiles can be resold.
        </p>
      </div>

      <div class="main">
        <h1 class="title"><span>MARKET</span>TILES <br /></h1>
      </div>
      <div class="blocks">
        <div class="none"></div>
        <a
          v-for="token in alltokens"
          :href="base + token"
          :key="token"
          class="block"
          target="_blank"
        >
          <div>
            <p class="block-price">0.1</p>
            <p class="block-price-dollar">$416</p>
          </div>
          <div class="buy-now-link">Buy now!</div>
        </a>

        <div class="none"></div>
      </div>
    </div>
    <div class="footer">
      <p>© 2021 10 Tiles LTD.</p>
    </div>
  </div>
</template>

<script>
// [] Connect to Smart Contract
// [] Fazer as calls do Smart Contract #methods
import Web3 from 'web3'
import json from '~/build/contracts/Tiles.json'
import TruffleContract from 'truffle-contract'

export default {
  data() {
    return {
      headers: [
        {
          text: 'Id',
          value: 'id',
        },
        {
          text: 'Atividades',
          value: 'content',
        },
        {
          text: 'Complete',
          value: 'complete',
        },
      ],
      web3Provider: null,
      account: null,
      web3: null,
      contracts: {},
      loading: true,
      tasks: [],
      newTaskCont: '',
      id: 0,
      tokenIds: [],
      alltokens: [],
      base: 'https://testnets.opensea.io/assets/0xc1d4e96cb49f4f0c7409640d6a9c015c92ef5efd/',
    }
  },
  created() {
    console.log('created')
    this.load()
  },
  methods: {
    async load() {
      await this.loadWeb3()
      await this.loadAccount(this)
      await this.loadContract(this)
      await this.renderTasks(this)
      this.loading = false
    },
    async loadWeb3() {
      this.web3 = window.web3
      // console.log('web3', this.web3)
      if (typeof this.web3 !== 'undefined') {
        this.web3Provider = this.web3.currentProvider
        this.web3 = new Web3(this.web3.currentProvider)
      } else {
        window.alert('Please connect to Metamask.')
      }
      // Modern dapp browsers...
      if (window.ethereum) {
        console.log('ethereum', window.ethereum)
        window.web3 = new Web3(ethereum)
        try {
          // Request account access if needed
          await ethereum.enable()
          // Acccounts now exposed
          web3.eth.sendTransaction({
            /* ... */
          })
        } catch (error) {
          // User denied account access...
        }
      }
      // Legacy dapp browsers...
      else if (window.web3) {
        App.web3Provider = web3.currentProvider
        window.web3 = new Web3(web3.currentProvider)
        // Acccounts always exposed
        web3.eth.sendTransaction({
          /* ... */
        })
      }
      // Non-dapp browsers...
      else {
        console.log(
          'Non-Ethereum browser detected. You should consider trying MetaMask!'
        )
      }
    },
    loadAccount: async (parent) => {
      // Set the current blockchain account
      let accounts = await ethereum.request({
        method: 'eth_requestAccounts',
      })
      console.log('Account', accounts)
      parent.account = accounts[0]
      console.log('0 Account', parent.account)
    },
    loadContract: async (parent) => {
      // Create a JavaScript version of the smart contract
      parent.contracts.TodoList = TruffleContract(json)
      parent.contracts.TodoList.setProvider(parent.web3Provider)

      // Hydrate the smart contract with values from the blockchain
      parent.todoList = await parent.contracts.TodoList.deployed()
      console.log('contract TILES', parent.todoList)
    },
    render: async (parent) => {
      // Prevent double render
      if (parent.loading) {
        return
      }

      // Update app loading state
      parent.loading = true

      // Render Account
      console.log('Render Account', parent.account)

      // Render Tasks
      await parent.renderTasks(parent)

      // Update loading state
      parent.loading = false
    },

    renderTasks: async (parent) => {
      // Load the total task count from the blockchain
      const taskCount = await parent.todoList.maxSupply()
      console.log('maxsupply:' + taskCount)

      parent.alltokens = await parent.todoList.asd()
      console.log('alltokens:' + parent.alltokens)

      parent.tokenIds = await parent.todoList.walletOfHolder(parent.account)
      console.log('tokenIds:' + parent.tokenIds)

      /*
      parent.tasks = [];
      for (var i = 1; i <= taskCount; i++) {
        // Fetch the task data from the blockchain
        const task = await parent.todoList.tasks(i);
        let taskJson = {
          id: task[0].toNumber(),
          content: task[1],
          complete: task[2],
        };
        console.log("Task", taskJson);
        parent.tasks.push(taskJson);
      }
      */
    },

    async createTask() {
      this.loading = true
      await this.todoList.createTask(this.newTaskCont, {
        from: this.account,
      })
      this.loading = false
      this.newTaskCont = ''
      this.renderTasks(this)
    },

    async toggleCompleted() {
      if (this.id > 0) {
        this.loading = true
        const taskId = this.id
        await this.todoList.toggleCompleted(taskId, {
          from: this.account,
        })
        this.renderTasks(this)
        this.loading = false
      }
    },
  },
}
</script>

<style lang='scss'>
.page-about {
  min-height: 100vh;
  height: 100%;
  background: rgb(9, 9, 126);
  background: linear-gradient(38deg, #09097e 24%, #510074 100%);
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
    color: rgba(255, 255, 255, 0.2);
    overflow: hidden;
  }
  .content {
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;

    background-image: url('~/assets/man.png');
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
          color: #00ffff;
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
        border: 2px dashed rgba(255, 255, 255, 0.5);
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
            content: url('~/assets/eth.png');
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
    background: linear-gradient(38deg, #09097e 80%, #af00ff 100%);
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

