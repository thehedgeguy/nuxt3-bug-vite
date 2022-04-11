<script lang="ts" setup>
import CoinbaseWalletSDK from "@coinbase/wallet-sdk";
import Web3 from "web3";

onMounted(() => {});

function connect() {
  const APP_NAME = "My Awesome App";
  const APP_LOGO_URL = "https://example.com/logo.png";
  const DEFAULT_ETH_JSONRPC_URL =
    "https://mainnet.infura.io/v3/<YOUR_INFURA_API_KEY>";
  const DEFAULT_CHAIN_ID = 1;

  // Initialize Coinbase Wallet SDK
  const coinbaseWallet = new CoinbaseWalletSDK({
    appName: APP_NAME,
    appLogoUrl: APP_LOGO_URL,
    darkMode: false,
  });

  // Initialize a Web3 Provider object
  const ethereum = coinbaseWallet.makeWeb3Provider(
    DEFAULT_ETH_JSONRPC_URL,
    DEFAULT_CHAIN_ID
  );

  // Initialize a Web3 object
  const web3 = new Web3(ethereum as any);

  // Use eth_requestAccounts
  ethereum.request({ method: "eth_requestAccounts" }).then((response) => {
    const accounts: string[] = response as string[];
    console.log(`User's address is ${accounts[0]}`);

    // Optionally, have the default account set for web3.js
    web3.eth.defaultAccount = accounts[0];
  });
}
</script>

<template>
  <div>
    <button @click="connect">Connect coinbase</button>
  </div>
</template>
