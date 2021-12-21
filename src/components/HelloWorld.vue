
<template>
  <div>
test hello v4
  <button @click="action">Action</button>
  {{log}}
  {{log2}}
  </div>
</template>

<script>
/* eslint-disable */
// https://web3js.readthedocs.io/en/v1.2.11/web3.html
/* Web3.modules
> {
    Eth: Eth(provider),
    Net: Net(provider),
    Personal: Personal(provider),
    Shh: Shh(provider),
    Bzz: Bzz(provider),
} */
// https://npm.io/package/@walletconnect/web3-provider
//  Get Accounts
/* const accounts = await web3.eth.getAccounts();

//  Get Chain Id
const chainId = await web3.eth.chainId();

//  Get Network Id
const networkId = await web3.eth.net.getId();

// Send Transaction
const txHash = await web3.eth.sendTransaction(tx);

// Sign Transaction
const signedTx = await web3.eth.signTransaction(tx);

// Sign Message
const signedMessage = await web3.eth.sign(msg);

// Sign Typed Data
const signedTypedData = await web3.eth.signTypedData(msg); */
import Web3 from "web3";
import Web3Modal from "web3modal";
import WalletConnectProvider from "@walletconnect/web3-provider";
 import { ref, onMounted } from 'vue'

export default {
  
  setup () {
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

        console.log('here 0');
            const web3Modal = new Web3Modal({
              network: "mainnet", // optional
              cacheProvider: false, // optional
              providerOptions // required
            });
              /*      web3Modal.cachedProvider = ""; // This is referring to your instance not the class
          localStorage.removeItem("WEB3_CONNECT_CACHED_PROVIDER"); */
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
      }

    return {
      action,
            action2,
      log,
      log2
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
