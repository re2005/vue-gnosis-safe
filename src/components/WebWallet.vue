<template>
    <div v-if="!isActivated">
        <button @click="connect">Connect Wallet</button>
    </div>
</template>
<script lang="ts" setup>
    import {
        CoinbaseWalletConnector,
        MetaMaskConnector,
        useBoard,
        useEthers,
        useWallet,
        WalletConnectConnector,
    } from 'vue-dapp';
    import { SafeConnector } from '@gnosis.pm/safe-apps-wagmi';

    const { address, isActivated, provider } = useEthers();
    const { connectWith } = useWallet();
    const { open } = useBoard();
    const infuraId = '';

    const chain = {
        order: 1,
        chainId: 5,
        name: 'Gnosis safe',
        color: '#5FA5F3',
        networkUrl: 'string',
        explorerUrl: 'https://goerli.etherscan.io/',
        rpcUrls: ['https://cloudflare-eth.com'],
    };

    const connectors = [
        new SafeConnector({}),
        new MetaMaskConnector({
            appUrl: 'http://localhost:3000',
        }),
        new WalletConnectConnector({
            qrcode: true,
            rpc: {
                1: `https://mainnet.infura.io/v3/${infuraId}`,
                4: `https://rinkeby.infura.io/v3/${infuraId}`,
            },
        }),
        new CoinbaseWalletConnector({
            appName: 'Vue Dapp',
            jsonRpcUrl: `https://mainnet.infura.io/v3/${infuraId}`,
        }),
    ];

    const connect = async () => {
        await connectWith(connectors[0] as any);
    };
</script>
