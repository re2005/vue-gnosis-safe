<template>
    <img alt="Vue logo" src="./assets/logo.png" />
    <div>
        <WebWallet />
        {{ address }}
    </div>
</template>

<script lang="ts" setup>
    import WebWallet from './components/WebWallet.vue';
    import { useEthers } from 'vue-dapp';

    const { address, balance, chainId, isActivated } = useEthers();
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
