<script setup lang="ts">
import { ethers } from "ethers";
import { onMounted, ref } from "vue";

const provider = new ethers.providers.JsonRpcProvider(
  "https://goerli-rollup.arbitrum.io/rpc"
);
const walletAddress = "0x30c3fDF579F8A0DAbbeE9AEFdaf64AAa39113260";

const loaded = ref(false);
const balanceString = ref("");

onMounted(() => {
  provider.getBalance(walletAddress).then((v) => {
    balanceString.value = ethers.utils.formatEther(v);
    loaded.value = true;
  });
});
</script>

<template>
  <main>
    <div v-if="loaded">
      Balance for wallet {{ walletAddress }}: {{ balanceString }} ETH
    </div>
    <div v-if="!loaded">…</div>
  </main>
</template>

<style scoped></style>
