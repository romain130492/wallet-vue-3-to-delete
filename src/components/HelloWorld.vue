
<template>
  <div>
test hello
  <button @click="action">Action</button>
  {{log}}
  </div>
</template>

<script>
/* eslint-disable */
import Web3 from "web3";
import Web3Modal from "web3modal";
import WalletConnectProvider from "@walletconnect/web3-provider";
 import { ref, onMounted } from 'vue'

export default {
  
  setup () {
    let log = ref('test')
       const action = async () =>{

          try {
            

            console.log('action');
            const providerOptions = {
              walletconnect: {
                  package: WalletConnectProvider, // required
                  options: {
                    infuraId: "69b27f2252994134974da9602463680f" // required
                  }
                }
          };

            const web3Modal = new Web3Modal({
              network: "mainnet", // optional
              cacheProvider: true, // optional
              providerOptions // required
            });

            const provider = await web3Modal.connect();
            
             provider.on("connect", (info) => {
            console.log(info,'info ');
            log.value = info;
          });
             provider.on("accountsChanged", (accounts) => {
                    log.value = accounts;
              console.log(accounts,'accounts');
            });

            provider.on("disconnect", (error) => {
              console.log(error,'the error111');
            log.value = error?error.message:error;
            });
            const web3 = new Web3(provider);


          } catch (error) {
            console.log(error,'the error????');
            log.value = error?error.message:error;
      
          }
      }

    return {
      action,
      log
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
