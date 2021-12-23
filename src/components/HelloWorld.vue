
<template>
  <div>
test hello v7
 <button @click="action">Action 1</button>
  {{log}} 

 <button @click="connectWalletMetamask">  connectWalletMetamask</button>

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
 const Moralis = require('moralis');

import Matic from "maticjs"


/* eslint-disable */
export default {
  
  setup () {

    Moralis.initialize('xeefjYVA5VAUT2XHxLnax6v25kM6jLoQJWvzIoJVPkJfyo9rpyUnt4RtAKjVmjQi');
    Moralis.serverURL = 'https://qqmhgwptk8vf.usemoralis.com:2053/server';
  const init =async  () =>{
    window.web3 = await Moralis.Web3.enable();
    console.log(window.web3,'moralis web3');
  }
  init()

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
    

/* const switchRequest = () => {
  return window.ethereum.request({
  method: "wallet_switchEthereumChain",
  params: [{ chainId: "0x1" }],
  });
};

const addChainRequest = () => {
return window.ethereum.request({
  method: "wallet_addEthereumChain",
      params: [
        {
        chainId: "0xa86a",
        chainName: "Avalanche Mainnet",
        rpcUrls: ["https://api.avax.network/ext/bc/C/rpc"],
        blockExplorerUrls: ["https://cchain.explorer.avax.network/"],
        nativeCurrency: {
        name: "AVAX",
        symbol: "AVAX",
        decimals: 18,
        },
      },
    ],
  });
};

export const switchNetwork = async () => {
  if (window.ethereum) {
  try {
  await switchRequest();
    } catch (error: any) {
    if (error.code === 4902) {
      try {
        await addChainRequest();
        await switchRequest();
      } catch (addError) {
      console.log(error);
      }
    }
    console.log(error);
    }
  }
}; */

   const initListeners = () => {
    // @ts-ignore
      const { ethereum } = window;
      ethereum.on('accountsChanged', (accounts) => {
        console.info('account changed', accounts);
      });
      ethereum.on('connect', () => {
        console.info('connect');
      });
      ethereum.on('disconnect', () => {
        console.info('connect');
      });
    };

        const connectWallet = async (walletProvider='metamask') => {
      console.log('connectWallet')
      try {

        let walletID;
          walletID = await connectWalletMetamask();
        if (!walletID) {
          throw Error('connectWallet: no walletID');
        }
        currentWallet.value = walletID;
        await updateWalletDb(walletID, walletProvider, isWalletTokenAdded);
        updateWalletProviderSelected(walletProvider);
        ctx.emit('wallet-connected', {walletID, isManual:false});
      } catch (error) {
        console.error('connectWallet(), error:', error);
      }
    };

   const addGtrTokenToWallet = async () => {
      try {
        // @ts-ignore
        const { ethereum } = window;
        if (!ethereum) {
          throw Error('addGtrTokenToWallet(): ethereum is null');
        }
   
        return ethereum
          .request({
            method: 'wallet_watchAsset',
            params: {
              type: 'ERC20',
              options: {
                address: '0x8ff36c854d901620476230dd8fba6780ad44c58a', // The address that the token is at.
                symbol: 'GTR', // A ticket symbol or shorthand, up to 5 chars.
                decimals: 18, // The number of decimals in the token
                image: 'https://gigs.gig-gly.com/icons/gig-gly-coin2.png', // A string url of the token logo // giggly-color.png
              },
            },
          })
          .then((success) => {
            if (success) {
              console.log('GTR token successfully added to wallet!', success);
              return true;
            }
            return false;
          })
          .catch(console.error);
      } catch (error) {
        throw Error(`addGtrTokenToWallet(): ${error}`);
      }
    };


    const connectWalletMetamask = async () => {
      try {
        // @ts-ignore
        //const { ethereum } = window;
        const ethereum = window.web3.eth;
        console.log(ethereum,'the etheumr here');
        if (!ethereum) {
          feedbackWalletProvider.value = 'You need to install <a target=\'_blank\' href=\'https://metamask.io/\'>Metamask.</a>';
          return;
        }
        // const isWalletTokenAdded = await addGtrTokenToWallet();
        console.log('enable metamast');
        //await ethereum.enable();
        initListeners();
        const accounts = await ethereum.request({
          method: 'eth_requestAccounts',
        });
        console.log(accounts ,'accounts accounts ');
        return accounts[0];
      } catch (error) {
        console.error(`connectWalletMetamask(): ${error}`);
        return null;
      }
    };
    const action2 = async()=>{
      try {
console.log('new???');
        //  Create WalletConnect Provider
        const provider = new WalletConnectProvider(
          {
        rpc: {
          137:'https://matic-mainnet.chainstacklabs.com'
        },
     /*    chainId: [137], */
        //infuraId: "69b27f2252994134974da9602463680f" 
      }
          
          
        /*   {
      
          rpc: {
                  56: 'https://bsc-dataseed.binance.org/',
                },
                network: 'binance',
                chainId: 56,
          infuraId:  "69b27f2252994134974da9602463680f" , 
        }   */     );

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

       const action = async () =>{

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
      } 

    return {
   action, 
            action2,
            connectWalletMetamask,
            initListeners,
   
      log,
      log2
    }
  }
}
</script>

<style lang="scss" scoped>

</style>



