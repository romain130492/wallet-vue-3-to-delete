<template>
  <div>
test hello
  <button @click="action">Action</button>
  </div>
</template>

<script>
/* eslint-disable */
import Web3 from "web3";
import Web3Modal from "web3modal";
export default {
  
  setup () {
       const action = async () =>{
      console.log('action');
      const providerOptions = {
      /* See Provider Options Section */
    };

    const web3Modal = new Web3Modal({
      network: "mainnet", // optional
      cacheProvider: true, // optional
      providerOptions // required
    });

    const provider = await web3Modal.connect();

    // Subscribe to accounts change


    const web3 = new Web3(provider);

      }

    return {
      action
    }
  }
}
</script>

<style lang="scss" scoped>

</style>