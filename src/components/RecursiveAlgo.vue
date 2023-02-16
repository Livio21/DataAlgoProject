<template>
    <div class="bg-gray-100 rounded-3xl p-10 flex flex-col gap-5">
        <div class="">
            <h1 class="font-bold text-5xl pb-5 text-slate-800">Recursive Algorithms (Multiplication)</h1>
            <span class="text-slate-600 font-semibold ml-3 mb-3">About</span>
            <p class=" bg-white rounded-3xl p-4 shadow-sm text-slate-800">This function works by repeatedly adding m to itself n - 1
                times. The function uses recursion to keep track of the
                number of times m should be added to itself, until n becomes 0 or 1. When n is 0, the function returns
                0, and when n is
                1, the function returns m.</p>

        </div>
        <div class="grid grid-cols-2 grid-rows-2 grid-flow-dense shadow-md bg-white rounded-3xl">
            <div class=" flex min-h-full  shadow-sm relative border-r-2 border-b-2">
                <input type="number" name="" id=""
                    class="text-center w-full h-full text-6xl  rounded-3xl font-bold text-slate-600  focus:outline-none  "
                    min="0" v-model="number1">
                <div
                    class="grid grid-flow-col absolute top-0 right-0 sm:grid-flow-row h-full  font-bold text-2xl  divide-x-2 md:divide-x-0 md:divide-y-2 ">
                    <button class="p-4 hover:bg-gray-100 active:bg-gray-200 " @click="number1++">+</button>
                    <button class="p-4 hover:bg-gray-100 active:bg-gray-200" @click="number1--">-</button>
                </div>
            </div>
            <div class="flex min-h-full h-36  shadow-sm relative border-b-2">
                <input type="number" name="" id=""
                    class="text-center w-full h-full text-6xl rounded-3xl  font-bold text-slate-600  max-w-fit focus:outline-none  "
                    min="0" v-model="number2">
                <div
                    class="grid grid-flow-col absolute top-0 right-0 sm:grid-flow-row h-full  font-bold text-2xl  divide-x-2 md:divide-x-0 md:divide-y-2 ">
                    <button class="p-4 hover:bg-gray-100 active:bg-gray-200 " @click="number2++">+</button>
                    <button class="p-4 hover:bg-gray-100 active:bg-gray-200" @click="number2--">-</button>
                </div>
            </div>
            <div class="w-full border-r-2 ">
                <span class="text-xl font-semibold p-5 text-slate-600 ">Result:</span>
                <p class="p-5 text-6xl  text-slate-600 font-bold text-center">
                    {{ result }}
                </p>
            </div>
            <button class=" p-3 rounded-br-3xl text-slate-50 sm:text-2xl font-semibold shadow-sm row-span-1 
                col-span-1 transition duration-100 ease-in-out bg-blue-500 hover:bg-blue-600 active:bg-blue-700"
                @click="multiply(number1, number2)">Multiply</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const number1 = ref(0);
const number2 = ref(0);
const result = ref(0);

// Recursive function to compute the product of two positive integers, m and n, using only addition and subtraction.
function multiply(m, n) {
    // base case
    if (n === 0) {
        return 0;
    }

    // recursive case
    return result.value = (m + multiply(m, n - 1));
}

</script>

<style lang="scss" scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}
</style>