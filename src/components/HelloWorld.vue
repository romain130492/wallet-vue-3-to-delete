
<template>
  <div>
test hello v5
<!--   <button @click="action">Action</button>
  {{log}} -->

    <button @click="action2">Action2</button>
{{log}} 
      {{log2}}

  </div>
</template>

<script>
/* eslint-disable */
import Web3 from "web3";
import Web3Modal from "web3modal";
import WalletConnectProvider from "@walletconnect/web3-provider";
 import { ref, onMounted } from 'vue'

import Matic from "maticjs"


/* eslint-disable */
export default {
  
  setup () {

/*     const maticProvider = new WalletConnectProvider(
  {
    host: `https://rpc-mumbai.matic.today`,
    callbacks: {
      onConnect: console.log('connected'),
      onDisconnect: console.log('disconnected!')
    }
  }
)

const ropstenProvider = new WalletConnectProvider({
    host: `https://ropsten.infura.io/v3/70645f042c3a409599c60f96f6dd9fbc`,
    callbacks: {
      onConnect: console.log('connected'),
      onDisconnect: console.log('disconnected')
    }
  })


const maticWeb3 = new Web3(maticProvider)
const ropstenWeb3 = new Web3(ropstenProvider) */



    let log = ref('test')
    let log2 = []
    
    const action2 = async()=>{
      try {

        //  Create WalletConnect Provider
        const provider = new WalletConnectProvider({
          infuraId:  "69b27f2252994134974da9602463680f" , // Required
        });

        //  Enable session (triggers QR Code modal)
        await provider.enable();

        //  Create Web3
        const web3 = new Web3(provider);
        console.log(web3,'the web3 test');
        log2.push('test????')
        log.value='rorororo'
        log2.push(Object.keys(web3.eth))  
        console.log(Object.keys(web3.eth) ,'Object.keys(web3)[0] '); 
        console.log(log2,'lgos2');
        console.log(web3.eth.requestAccounts,'web3.ethweb3.ethweb3.eth');
        const accounts = await web3.eth.requestAccounts()
        console.log(accounts,'the acocunts new 2');

        // Subscribe to accounts change
        provider.on("accountsChanged", (accounts) => {
          console.log(accounts);
        });

        // Subscribe to chainId change
        provider.on("chainChanged", (chainId) => {
          console.log(chainId);
        });

        // Subscribe to session connection
        provider.on("connect", () => {
          console.log("connect");
        });

        // Subscribe to session disconnection
        provider.on("disconnect", (code, reason) => {
          console.log(code, reason);
        }); 
      } catch (error) {
        console.log(error,'error');
      }
    }
    
     /*   const action = async () =>{

          try {
     
            console.log('action');
            const providerOptions = {
              walletconnect: {
                  package: WalletConnectProvider, // required,
                    options: {
                      rpc: {
                        0x89: "https://matic-mainnet.chainstacklabs.com",
                      },
                      network: "polygon-mainet",
                    },
                  options: {
                    infuraId: "69b27f2252994134974da9602463680f" // required
                  }
                }
          };

        console.log('here 0');
            const web3Modal = new Web3Modal({
              network: "mainnet", // optional
              cacheProvider: false, // optional
              providerOptions // required
            });
 
        console.log('here 1');
            const provider = await web3Modal.connect();
            console.log('here 2');
             provider.on("connect", (info) => {
                console.log(info,'info ');
                log.value = info;
              });
             provider.on("accountsChanged", (accounts) => {
              log.value = accounts;
              console.log(accounts,'accounts');
            });
            provider.on("chainChanged", (chainId) => {
              console.log(chainId,'chianidn');
            });

            provider.on("disconnect", (error) => {
              console.log(error,'the error111');
            log.value = error?error.message:error;
            });
            const web3 = new Web3(provider);
            // that one above works !!!!!!!!!!! on mobile and desktop tamade
            const accounts = await web3.eth.getAccounts();
            console.log(web3,'web3');
            //log2.push(web3)
            console.log(accounts,'the accounts here???');
            console.log(web3.eth,'web3.eth');
            //const accounts = await web3.eth.requestAccounts()
            console.log(accounts[0],'accounts');
            log.value= accounts
            log2.push(accounts)

          } catch (error) {
            console.log(error,'the error????');
            log.value = error?error.message:error;
      
          }
      } */

    return {
/*       action, */
            action2,
   
      log,
      log2
    }
  }
}
</script>

<style lang="scss" scoped>

</style>



