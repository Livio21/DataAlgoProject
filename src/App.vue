<template>
  <div class="mx-auto my-5 flex flex-col gap-10 items-center max-w-6xl  rounded-3xl p-10 min-h-screen ">
    <page-header></page-header>
    <div class="" id="nav">
      <div class="p-5 bg-gray-100 rounded-3xl flex items-center justify-center text-xl text-slate-700 gap-5 ">
        <span class="text-slate-800 text-xl font-bold pl-6 ">Navigation:</span>
        <button @click="selected = 'CeaserCypher'"
          class="font-semibold bg-white rounded-xl px-5 py-2 shadow-sm active:scale-95 active:shadow-none transition-all duration-100 ease-in">Ceasar
          Cypher</button>
        <button @click="selected = 'RecAlgo'"
          class="font-semibold bg-white rounded-xl px-5 py-2 shadow-sm active:scale-95 active:shadow-none transition-all duration-150 ease-in-out">Product
          of two
          Intigers</button>
        <button @click="selected = 'HeapSort'"
          class="font-semibold bg-white rounded-xl px-5 py-2 shadow-sm active:scale-95 active:shadow-none transition-all duration-150 ease-in-out">Heap
          Sort</button>
      </div>
    </div>
    <transition-group name="v">
      <CeaserCypher v-if="selected == 'CeaserCypher'"></CeaserCypher>
      <RecursiveAlgo v-if="selected == 'RecAlgo'"></RecursiveAlgo>
      <HeapSort v-if="selected == 'HeapSort'"></HeapSort>
    </transition-group>
    <PageFooter></PageFooter>
  </div>
</template>

<script setup>
import CeaserCypher from './components/CeaserCypher.vue';
import RecursiveAlgo from './components/RecursiveAlgo.vue';
import PageFooter from './components/PageFooter.vue';
import PageHeader from './components/PageHeader.vue';
import HeapSort from './components/HeapSort.vue';
import { ref } from 'vue';

const selected = ref('HeapSort');



</script>

<style lang="scss" scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.125s ease-in-out;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>