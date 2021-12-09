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
        <div>
          <button @click="wallet()">get wallet</button>
          {{history}}
        </div>
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
import pinata from '../service/pinata'
import ar from '../service/ar'
import arweave from '../service/arweave'
export default {
  async fetch() {
    // pinata.getPinata(this.$axios)

  },
  computed: {
    history() {
      return this.$arGetDefaultWalletTransactionHistory ? this.$arGetDefaultWalletTransactionHistory.map(item => item.enrichedTransaction.dataString) : []
    }
  },
  methods: {
    async wallet(){
      const key = {"kty":"RSA","n":"8Ikjy2KQA4-YJqdMWF3g4cfrmpnFSXXj5Jq9v5noawMbxyAEu8GQWfXopQ4A9i4L_kDfhXi-g01tKL2q3P2lYBqqr1UVIqqJnUSnXf1UXqHZY4ng25GECGAyLSlvaNzqKLhWos5p9uLRXyBWX4LKazwuCEMLKEPIAJ-6Jk7MdPbkV5SG40U8LQe4YGiyzAO2IWnoKNUZKJbNBuL9ufJTyl6Ty7fcnXIaodh5v-TEQo_ywFjJIHzkR0Xd0Ccxh0ptLjLB_fricc4gE7rp-4ySe1rfIAAJkDLg615ArT6_n80B76gL1WhVE_jMDGSslR2ImsFor59rPGTIU_SMmTVtfVfq-r8nTS32Pci8Pyf7yBolZA2T-AtPQrO3cpy0ECbwRfnaxoC3TufxKb91fLws8Howli0b8BXA12RfFKbvB2yPyMsognJYj6Q3T2Qr2jWgNTEZQ8hP_um7dFBZzb9Dy2yecQ8HCIq3IxSqb1gAB_LMj-nrAtvFOxarJwMEveFgkEjbut_pzwxbrfRURXbzcBT4Ondf30YolPp_f2v-vyaByeQRS67fqeLE-9rQg6rBOgjbW0fKUtAvBQr-ftjsLKF-h0VuY0DjOzr5qmdSZzzk7XTr8uqDURHOTcritzJMuGrtk0Ez4L3Grxj4bx5QLhR3yFQS5zTXdOptv90wn3M","e":"AQAB","d":"uV1mSVGOnD_nyDn7Oso2CKkxpvXDtQX19vFNMz_ffcBqgrzpCOx1Wu6IN9Kf6Re5RFooJ0rSvotHiTMJXr7V2EcUrIPMAugbnygONv-IKlleFzhlIbB1aKMBaA5bfhtpFLJiiZq6zHklUsKv7XD0n0lETDemfIQnuFtfcDAfni-57shWXwS3CBi__QQSbeiaTgu4zubSOZZlMF5zm_3klrrl-QObL3aEkZ8qzDf3Czi1oYeKj8_PeCGee9AIejNgCk8xcpIKOhvYWnwb3zAInql788Qzmn2rGZeMDjaiI_sv98mwPOjnT7nXPeHDojKdWG2eSGF5mZQtUY3PYC5tTcGgdigQjWAjewQgF-eAl_knZ2K2_C6tqaE6mQpkOqdRkA_ppGcCPm-dWbFuaXr8TigbMkcXXrGpLtTyoXrKcuuv_NWCAWWfW4tBv4RV-_4tEjYrx1HG-GQe_mZSlPuTGk26T7sv5dvi22hXGQxB2GhT92q6NJSQcqPHhPmTzM3uPVzat4mpEPB0LTdE3qToD_PK4mBOo4vvUSKGmE4vMXq-iqxlYsOWjoSIcFQvE3cLjmWmyDi_jxDrqTFe9FPrObCzLT1LjbwsqtGu_4X-W3P3C9FlM_yVlxNSCDqEOQiP03EJcsm-QWPq97gJiGFtoevOVfTrtvsi77G6n6O3tjk","p":"-HN3R1ZwJPCFsu4kpWQWtl5dVadGnn2GdDw-f1urXT0OntDVl8XcEkqUodrl7r8lV9qzsq7HsD6d8oeq0TWw1VvNbhILfdIPARdsb1P2Rhataq74zRWnVXOgGA-GkR9NVgerRqiiRxf4Xz3lLiS9qbOLGe1H4ImhO7mAlXE0Tbv8-SXdiiVyu4hN6TonoV1QQ4z_OrFWyTZ0X2regPX4sw0LKEV-meeXFemy3o7FpN06UKr1RdH6pj7yOwBFouuZNWjuHV9sAzssdqsqMAlZg5CxETJpcr0P02GniCM0Mi23AKVI5_NW-xAkn7cJU7L_pbZLpA5F2-uJZP7RiRKbpw","q":"99gbFV2ux2WyNRWJv0IwnjgHBuzTS-nTaGu8vowQm4MTa6K2lwxbSmqytA-IK_-oY_RWsb_GfME-Cpuau0KWdkLoKRUm_yVSkFAPxjz507lwUgpiMEgXybBKErR-SZmOpNEGqnrZtlxT_O_r0Tqlb9371QQn9O_tgnjjF0vXoKd-W0Bts-wOc4Az7Bcz0aERjNLU8-Dh4Oxx49MKAsD2Sms73hN9B8iQID-wTgO7d7xiSp7wil9sr1rtqwkgxRJQR_wpzsHefcJ2DAlGbn7SPBygjAGmIMKprUigs9njEhSifgqIchLl3rtJgwbe_zaBghT0zotJ5BS5iMwiYN-nVQ","dp":"WN9c1HzcAqqy-K1tGGh0I2of8uqyPTFjriJ6rK4K34BewXqsXO0e6sAY6MjXpQ5k-kc2Ln2M2sObVk0nUkzlY3zCQFReHfTM_zP0yuH631lvUREj2KCdSdjhdJnhJfpPfK2jm9PosIungdIvL9FestyRroWNR4mTzjxt_YcQEZpkRG9CDw-UOfbo_7uYv4UUmAVQqxsSk0lSWWtuCi1yeAH7cr1hKwaHqgP9wtTJaE7mdEKjGAWjpmIv3eEcB8pE9LEDNCiVB5bcMdrKbYJ6rbBNVnx08eElTxTIi88j9asaojV9ndMS0x4UK7masYD_J7TM2_NrE97uN91a8LBiUw","dq":"93dLC5lf826icoiP4m1XmBM_SPXcwFa3pPK2Idg-mNhW4skz4TwQRwykZE-B2tTJsQv-KDrhGB3nMbZO2B1TmL-Tibm6F1aPytJ1_a1Skcn90ZzWj3jcb6DbRTP9SMXPfNfM_RnvGju0DMEOR_pzx2_xjK86qkGKeBT2QoOSyLGU484_-z9-6mqe7WP5dJ2LpX257cykHO5ZhW5p93fuMz5BJ6tz0vq6lcih5DOr0pFB31o1uSQwpCJ5XqadlsiDamzo3a4L1qv9LGVycs-kYSsATusyklFsFD6JXyr2pE4ANTOVK7mc1jlQ3EhXDqLAyz7bdQP1AoyC-IlC5lFKhQ","qi":"EWaaOopMtLf_hmT_2RKNb3A-MO1TO-uJuFHXf-uIwTNaxhmJv6s9dHVn_62ky7OdYXO90I6GtTEcRdRjgUrOlRNgpr9cECplyz1GI_kMghjK4n2pUbV3vS-eqP6Hfyl8s5L2mQPDE-zkIV_y8ikGiQ3pY0urRmMPvMBMBgzhCeFpXFvAhZLMEXo-EbSzEUxEnqkKH-fhjFyhCZEfZcGCvbhRyWymkB6UGDXKEls5gOwPrSaHLLyYTSJBxqLuC50Bmf_tOvCNb1eYHUL2Blj1jXZEt-Gy9_lnnoJRhzUr4WhA-b5ILnwCQhzb7cmK9HMToWofCPOz0-UpKhpjUgRffw"};

      // this.$arImportWallet({
      //   name: 'the name for your wallet', // not mandatory, the default is 'null'
      //   isDefault: true, // not mandatory, the default is false.
      //   jwt: key, // mandatory, throws an error if the jwt is not specified
      // })

      // await this.$arGenerateWallet({
      //   name: 'the name for your wallet', // not mandatory, the default is 'null'
      //   isDefault: false, // not mandatory, the default is false.
      // })
      const history = this.$arGetDefaultWalletTransactionHistory
      console.log(history.map(item => item.enrichedTransaction.dataString))
      console.log(this.$arGetWallets, this.$arGetDefaultWallet)

      console.log(await this.$arUtilsTransactionGetData(
        'Wg5V5vDOCPrieVduWDH15mqU430HsjOkpLdUHTyar6E', // the id of the transaction
        true, // if set to true decode the transaction data. The default is false
        true
        // if set to true decode the transaction data into a string. The default is false
      ))
    }
  },
  async mounted() {
    // await this.$arImportWallet({
    //   jwk: {"kty":"RSA","n":"8Ikjy2KQA4-YJqdMWF3g4cfrmpnFSXXj5Jq9v5noawMbxyAEu8GQWfXopQ4A9i4L_kDfhXi-g01tKL2q3P2lYBqqr1UVIqqJnUSnXf1UXqHZY4ng25GECGAyLSlvaNzqKLhWos5p9uLRXyBWX4LKazwuCEMLKEPIAJ-6Jk7MdPbkV5SG40U8LQe4YGiyzAO2IWnoKNUZKJbNBuL9ufJTyl6Ty7fcnXIaodh5v-TEQo_ywFjJIHzkR0Xd0Ccxh0ptLjLB_fricc4gE7rp-4ySe1rfIAAJkDLg615ArT6_n80B76gL1WhVE_jMDGSslR2ImsFor59rPGTIU_SMmTVtfVfq-r8nTS32Pci8Pyf7yBolZA2T-AtPQrO3cpy0ECbwRfnaxoC3TufxKb91fLws8Howli0b8BXA12RfFKbvB2yPyMsognJYj6Q3T2Qr2jWgNTEZQ8hP_um7dFBZzb9Dy2yecQ8HCIq3IxSqb1gAB_LMj-nrAtvFOxarJwMEveFgkEjbut_pzwxbrfRURXbzcBT4Ondf30YolPp_f2v-vyaByeQRS67fqeLE-9rQg6rBOgjbW0fKUtAvBQr-ftjsLKF-h0VuY0DjOzr5qmdSZzzk7XTr8uqDURHOTcritzJMuGrtk0Ez4L3Grxj4bx5QLhR3yFQS5zTXdOptv90wn3M","e":"AQAB","d":"uV1mSVGOnD_nyDn7Oso2CKkxpvXDtQX19vFNMz_ffcBqgrzpCOx1Wu6IN9Kf6Re5RFooJ0rSvotHiTMJXr7V2EcUrIPMAugbnygONv-IKlleFzhlIbB1aKMBaA5bfhtpFLJiiZq6zHklUsKv7XD0n0lETDemfIQnuFtfcDAfni-57shWXwS3CBi__QQSbeiaTgu4zubSOZZlMF5zm_3klrrl-QObL3aEkZ8qzDf3Czi1oYeKj8_PeCGee9AIejNgCk8xcpIKOhvYWnwb3zAInql788Qzmn2rGZeMDjaiI_sv98mwPOjnT7nXPeHDojKdWG2eSGF5mZQtUY3PYC5tTcGgdigQjWAjewQgF-eAl_knZ2K2_C6tqaE6mQpkOqdRkA_ppGcCPm-dWbFuaXr8TigbMkcXXrGpLtTyoXrKcuuv_NWCAWWfW4tBv4RV-_4tEjYrx1HG-GQe_mZSlPuTGk26T7sv5dvi22hXGQxB2GhT92q6NJSQcqPHhPmTzM3uPVzat4mpEPB0LTdE3qToD_PK4mBOo4vvUSKGmE4vMXq-iqxlYsOWjoSIcFQvE3cLjmWmyDi_jxDrqTFe9FPrObCzLT1LjbwsqtGu_4X-W3P3C9FlM_yVlxNSCDqEOQiP03EJcsm-QWPq97gJiGFtoevOVfTrtvsi77G6n6O3tjk","p":"-HN3R1ZwJPCFsu4kpWQWtl5dVadGnn2GdDw-f1urXT0OntDVl8XcEkqUodrl7r8lV9qzsq7HsD6d8oeq0TWw1VvNbhILfdIPARdsb1P2Rhataq74zRWnVXOgGA-GkR9NVgerRqiiRxf4Xz3lLiS9qbOLGe1H4ImhO7mAlXE0Tbv8-SXdiiVyu4hN6TonoV1QQ4z_OrFWyTZ0X2regPX4sw0LKEV-meeXFemy3o7FpN06UKr1RdH6pj7yOwBFouuZNWjuHV9sAzssdqsqMAlZg5CxETJpcr0P02GniCM0Mi23AKVI5_NW-xAkn7cJU7L_pbZLpA5F2-uJZP7RiRKbpw","q":"99gbFV2ux2WyNRWJv0IwnjgHBuzTS-nTaGu8vowQm4MTa6K2lwxbSmqytA-IK_-oY_RWsb_GfME-Cpuau0KWdkLoKRUm_yVSkFAPxjz507lwUgpiMEgXybBKErR-SZmOpNEGqnrZtlxT_O_r0Tqlb9371QQn9O_tgnjjF0vXoKd-W0Bts-wOc4Az7Bcz0aERjNLU8-Dh4Oxx49MKAsD2Sms73hN9B8iQID-wTgO7d7xiSp7wil9sr1rtqwkgxRJQR_wpzsHefcJ2DAlGbn7SPBygjAGmIMKprUigs9njEhSifgqIchLl3rtJgwbe_zaBghT0zotJ5BS5iMwiYN-nVQ","dp":"WN9c1HzcAqqy-K1tGGh0I2of8uqyPTFjriJ6rK4K34BewXqsXO0e6sAY6MjXpQ5k-kc2Ln2M2sObVk0nUkzlY3zCQFReHfTM_zP0yuH631lvUREj2KCdSdjhdJnhJfpPfK2jm9PosIungdIvL9FestyRroWNR4mTzjxt_YcQEZpkRG9CDw-UOfbo_7uYv4UUmAVQqxsSk0lSWWtuCi1yeAH7cr1hKwaHqgP9wtTJaE7mdEKjGAWjpmIv3eEcB8pE9LEDNCiVB5bcMdrKbYJ6rbBNVnx08eElTxTIi88j9asaojV9ndMS0x4UK7masYD_J7TM2_NrE97uN91a8LBiUw","dq":"93dLC5lf826icoiP4m1XmBM_SPXcwFa3pPK2Idg-mNhW4skz4TwQRwykZE-B2tTJsQv-KDrhGB3nMbZO2B1TmL-Tibm6F1aPytJ1_a1Skcn90ZzWj3jcb6DbRTP9SMXPfNfM_RnvGju0DMEOR_pzx2_xjK86qkGKeBT2QoOSyLGU484_-z9-6mqe7WP5dJ2LpX257cykHO5ZhW5p93fuMz5BJ6tz0vq6lcih5DOr0pFB31o1uSQwpCJ5XqadlsiDamzo3a4L1qv9LGVycs-kYSsATusyklFsFD6JXyr2pE4ANTOVK7mc1jlQ3EhXDqLAyz7bdQP1AoyC-IlC5lFKhQ","qi":"EWaaOopMtLf_hmT_2RKNb3A-MO1TO-uJuFHXf-uIwTNaxhmJv6s9dHVn_62ky7OdYXO90I6GtTEcRdRjgUrOlRNgpr9cECplyz1GI_kMghjK4n2pUbV3vS-eqP6Hfyl8s5L2mQPDE-zkIV_y8ikGiQ3pY0urRmMPvMBMBgzhCeFpXFvAhZLMEXo-EbSzEUxEnqkKH-fhjFyhCZEfZcGCvbhRyWymkB6UGDXKEls5gOwPrSaHLLyYTSJBxqLuC50Bmf_tOvCNb1eYHUL2Blj1jXZEt-Gy9_lnnoJRhzUr4WhA-b5ILnwCQhzb7cmK9HMToWofCPOz0-UpKhpjUgRffw"} // mandatory, throws an error if the jwt is not specified
    // })
    // ar.sendToBundler()
    const key = {"kty":"RSA","n":"8Ikjy2KQA4-YJqdMWF3g4cfrmpnFSXXj5Jq9v5noawMbxyAEu8GQWfXopQ4A9i4L_kDfhXi-g01tKL2q3P2lYBqqr1UVIqqJnUSnXf1UXqHZY4ng25GECGAyLSlvaNzqKLhWos5p9uLRXyBWX4LKazwuCEMLKEPIAJ-6Jk7MdPbkV5SG40U8LQe4YGiyzAO2IWnoKNUZKJbNBuL9ufJTyl6Ty7fcnXIaodh5v-TEQo_ywFjJIHzkR0Xd0Ccxh0ptLjLB_fricc4gE7rp-4ySe1rfIAAJkDLg615ArT6_n80B76gL1WhVE_jMDGSslR2ImsFor59rPGTIU_SMmTVtfVfq-r8nTS32Pci8Pyf7yBolZA2T-AtPQrO3cpy0ECbwRfnaxoC3TufxKb91fLws8Howli0b8BXA12RfFKbvB2yPyMsognJYj6Q3T2Qr2jWgNTEZQ8hP_um7dFBZzb9Dy2yecQ8HCIq3IxSqb1gAB_LMj-nrAtvFOxarJwMEveFgkEjbut_pzwxbrfRURXbzcBT4Ondf30YolPp_f2v-vyaByeQRS67fqeLE-9rQg6rBOgjbW0fKUtAvBQr-ftjsLKF-h0VuY0DjOzr5qmdSZzzk7XTr8uqDURHOTcritzJMuGrtk0Ez4L3Grxj4bx5QLhR3yFQS5zTXdOptv90wn3M","e":"AQAB","d":"uV1mSVGOnD_nyDn7Oso2CKkxpvXDtQX19vFNMz_ffcBqgrzpCOx1Wu6IN9Kf6Re5RFooJ0rSvotHiTMJXr7V2EcUrIPMAugbnygONv-IKlleFzhlIbB1aKMBaA5bfhtpFLJiiZq6zHklUsKv7XD0n0lETDemfIQnuFtfcDAfni-57shWXwS3CBi__QQSbeiaTgu4zubSOZZlMF5zm_3klrrl-QObL3aEkZ8qzDf3Czi1oYeKj8_PeCGee9AIejNgCk8xcpIKOhvYWnwb3zAInql788Qzmn2rGZeMDjaiI_sv98mwPOjnT7nXPeHDojKdWG2eSGF5mZQtUY3PYC5tTcGgdigQjWAjewQgF-eAl_knZ2K2_C6tqaE6mQpkOqdRkA_ppGcCPm-dWbFuaXr8TigbMkcXXrGpLtTyoXrKcuuv_NWCAWWfW4tBv4RV-_4tEjYrx1HG-GQe_mZSlPuTGk26T7sv5dvi22hXGQxB2GhT92q6NJSQcqPHhPmTzM3uPVzat4mpEPB0LTdE3qToD_PK4mBOo4vvUSKGmE4vMXq-iqxlYsOWjoSIcFQvE3cLjmWmyDi_jxDrqTFe9FPrObCzLT1LjbwsqtGu_4X-W3P3C9FlM_yVlxNSCDqEOQiP03EJcsm-QWPq97gJiGFtoevOVfTrtvsi77G6n6O3tjk","p":"-HN3R1ZwJPCFsu4kpWQWtl5dVadGnn2GdDw-f1urXT0OntDVl8XcEkqUodrl7r8lV9qzsq7HsD6d8oeq0TWw1VvNbhILfdIPARdsb1P2Rhataq74zRWnVXOgGA-GkR9NVgerRqiiRxf4Xz3lLiS9qbOLGe1H4ImhO7mAlXE0Tbv8-SXdiiVyu4hN6TonoV1QQ4z_OrFWyTZ0X2regPX4sw0LKEV-meeXFemy3o7FpN06UKr1RdH6pj7yOwBFouuZNWjuHV9sAzssdqsqMAlZg5CxETJpcr0P02GniCM0Mi23AKVI5_NW-xAkn7cJU7L_pbZLpA5F2-uJZP7RiRKbpw","q":"99gbFV2ux2WyNRWJv0IwnjgHBuzTS-nTaGu8vowQm4MTa6K2lwxbSmqytA-IK_-oY_RWsb_GfME-Cpuau0KWdkLoKRUm_yVSkFAPxjz507lwUgpiMEgXybBKErR-SZmOpNEGqnrZtlxT_O_r0Tqlb9371QQn9O_tgnjjF0vXoKd-W0Bts-wOc4Az7Bcz0aERjNLU8-Dh4Oxx49MKAsD2Sms73hN9B8iQID-wTgO7d7xiSp7wil9sr1rtqwkgxRJQR_wpzsHefcJ2DAlGbn7SPBygjAGmIMKprUigs9njEhSifgqIchLl3rtJgwbe_zaBghT0zotJ5BS5iMwiYN-nVQ","dp":"WN9c1HzcAqqy-K1tGGh0I2of8uqyPTFjriJ6rK4K34BewXqsXO0e6sAY6MjXpQ5k-kc2Ln2M2sObVk0nUkzlY3zCQFReHfTM_zP0yuH631lvUREj2KCdSdjhdJnhJfpPfK2jm9PosIungdIvL9FestyRroWNR4mTzjxt_YcQEZpkRG9CDw-UOfbo_7uYv4UUmAVQqxsSk0lSWWtuCi1yeAH7cr1hKwaHqgP9wtTJaE7mdEKjGAWjpmIv3eEcB8pE9LEDNCiVB5bcMdrKbYJ6rbBNVnx08eElTxTIi88j9asaojV9ndMS0x4UK7masYD_J7TM2_NrE97uN91a8LBiUw","dq":"93dLC5lf826icoiP4m1XmBM_SPXcwFa3pPK2Idg-mNhW4skz4TwQRwykZE-B2tTJsQv-KDrhGB3nMbZO2B1TmL-Tibm6F1aPytJ1_a1Skcn90ZzWj3jcb6DbRTP9SMXPfNfM_RnvGju0DMEOR_pzx2_xjK86qkGKeBT2QoOSyLGU484_-z9-6mqe7WP5dJ2LpX257cykHO5ZhW5p93fuMz5BJ6tz0vq6lcih5DOr0pFB31o1uSQwpCJ5XqadlsiDamzo3a4L1qv9LGVycs-kYSsATusyklFsFD6JXyr2pE4ANTOVK7mc1jlQ3EhXDqLAyz7bdQP1AoyC-IlC5lFKhQ","qi":"EWaaOopMtLf_hmT_2RKNb3A-MO1TO-uJuFHXf-uIwTNaxhmJv6s9dHVn_62ky7OdYXO90I6GtTEcRdRjgUrOlRNgpr9cECplyz1GI_kMghjK4n2pUbV3vS-eqP6Hfyl8s5L2mQPDE-zkIV_y8ikGiQ3pY0urRmMPvMBMBgzhCeFpXFvAhZLMEXo-EbSzEUxEnqkKH-fhjFyhCZEfZcGCvbhRyWymkB6UGDXKEls5gOwPrSaHLLyYTSJBxqLuC50Bmf_tOvCNb1eYHUL2Blj1jXZEt-Gy9_lnnoJRhzUr4WhA-b5ILnwCQhzb7cmK9HMToWofCPOz0-UpKhpjUgRffw"};
    let myText =  "test generated key"

    // console.log("address", address);


    //

    // // Transaction ID gets updated after arweave.transactions.post, which is a bit unintuitive

    //

    // const generateKey = await arweave.wallets.generate()
    const generateKey = key
    console.log('key',generateKey)
    // arweave.wallets.jwkToAddress(generateKey).then((address) => {
    //   console.log('address',address);
    //   //1seRanklLU_1VTGkEk7P0xAwMJfA7owA1JHW5KyZKlY
    // });
    // const address = await arweave.wallets.jwkToAddress(generateKey);
    //
    // arweave.wallets.getBalance(address).then((balance) => {
    //   let winston = balance;
    //   let ar = arweave.ar.winstonToAr(balance);
    //
    //   console.log('winston',winston);
    //   //125213858712
    //
    //   console.log('ar', ar);
    //   //0.125213858712
    // });



    // const transaction = await arweave.createTransaction(
    //   {
    //     data: myText,
    //   },
    //   generateKey
    // );

    // await arweave.transactions.sign(transaction, generateKey);
    // const postResponse = await arweave.transactions.post(transaction);
    // console.log("post response", postResponse);
    // console.log("transaction ID", transaction.id);
    // const lastTransactionId = await arweave.wallets.getLastTransactionID(address);
    // console.log("lastTransactionId", lastTransactionId);
    //
    // // Read data back
    // const transactionData = await arweave.transactions.getData(transaction.id);
    // console.log(
    //   `transactions id: ${transaction.id}`,
    //   "transaction data",
    //   Buffer.from(transactionData, "base64").toString()
    // );
    // arweave.wallets.getLastTransactionID('PU2qbzk9UPRECxUCF9eE5Z3LpQezmKN7CazyXCmViww').then((transactionId) => {
    //   console.log('getLastTransactionID',transactionId);
    // });
  }
}
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
