<template>
    <div class="bg-gray-100 rounded-3xl shadow-md p-10 flex flex-col gap-5 items-center ">
        <div class="">
            <h1 class="font-bold text-5xl pb-5 text-slate-800">Heap sort</h1>
            <span class="text-slate-600 font-semibold ml-3 mb-3">About</span>
            <p class=" bg-white rounded-3xl p-4 shadow-sm text-slate-800">
                Heap sort is a comparison-based sorting algorithm. Heapsort can be thought of as an improved selection
                sort: like that algorithm, it divides its input into a sorted and an unsorted region, and it iteratively
                shrinks the unsorted region by extracting the largest element and moving that to the sorted region. The
                improvement consists of the use of a heap data structure rather than a linear-time search to find the
                maximum.
            </p>

        </div>
        <div class="">
            <div class="flex  divide-x-2 rounded-lg">
                <input type="number" class="p-4 text-xl" v-model="variable" >
                <button @click="addElement"
                    class="p-4 text-white bg-blue-500 rounded-r-xl font-semibold text-lg active:scale-95 active:shadow-none transition-all duration-150 ease-in-out">
                    Add</button>
            </div>
            <span id="err" class="p-3 text-red-500 font-semibold text-lg">{{ errMsg }}</span>

            <p class="p-3 bg-white my-3 rounded-xl">Array before: {{ prevArr }}</p>
            <p class="p-3 bg-white my-3 rounded-xl">Array after: {{ arr }}</p>
        </div>

        <div class="flex gap-3 items-end bg-white shadow-inner p-5 rounded-xl">
            <transition-group name="fade">
                <div v-for=" (el, index) in arr" :key="index">
                    <div id="block"
                        class="flex flex-col justify-between min-h-full bg-blue-500 w-[50px] text-center text-xl font-semibold rounded-t-lg "
                        :style="`height:${el * 5}px`">
                        <span class=" invert">{{ el }}</span>
                        <span class="bg-white ring-2 ring-blue-700">{{ index }}</span>
                    </div>
                </div>
            </transition-group>
        </div>
        <div class="flex gap-5">
            <button @click="btnAction(arr)"
                class="mt-10 text-white text-xl font-bold bg-green-500 rounded-xl px-5 py-2 shadow-sm active:scale-95 active:shadow-none transition-all duration-150 ease-in-out">Sort</button>
            <button @click="reset"
                class="mt-10 text-white text-xl font-bold bg-red-500 rounded-xl px-5 py-2 shadow-sm active:scale-95 active:shadow-none transition-all duration-150 ease-in-out">Reset</button>
        </div>

    </div>
</template>

<script setup>
import { ref } from 'vue';
//heap sort algorithm

const variable = ref(0);
const arr = ref([]);
const prevArr = ref([]);
const errMsg = ref('');

const reset = () => {
    arr.value = [];
    prevArr.value = [];
    variable.value = 0;
    errMsg.value = '';
}
const addElement = () => {
    if (variable.value == '') {
        errMsg.value = 'Empty input.'
        return;
    }
    else if (variable.value > 100) {
        errMsg.value = 'Input too large.'
        variable.value = 0
        return;
    }
    else {
        errMsg.value = '';
    }

    let t = variable.value;
    arr.value.push(Math.abs(t));
    prevArr.value.push(Math.abs(t));
    variable.value = '';
}

const heapify = (arr, n, i) => {
    let largest = i; // Initialize largest as root
    let l = 2 * i + 1; // left = 2*i + 1
    let r = 2 * i + 2; // right = 2*i + 2

    // If left child is larger than root
    if (l < n && arr[l] > arr[largest]) {
        largest = l;
    }

    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest]) {
        largest = r;
    }

    // If largest is not root
    if (largest != i) {
        let swap = arr[i];
        arr[i] = arr[largest];
        arr[largest] = swap;

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}


const heapSort = (arr) => {
    let n = arr.length;

    // Build heap (rearrange array)
    for (let i = Math.floor(n / 2) - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }

    // One by one extract an element from heap
    for (let i = n - 1; i >= 0; i--) {
        // Move current root to end
        let temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
    console.log(arr);
};

const btnAction = (a) => {
    if (a.length == 0) {
        errMsg.value = 'Empty array, add elements first.'
        return;
    }
    heapSort(a);

};

// const arr = [12, 11, 13, 5, 6, 7];
// heapSort(arr);
// console.log(arr);


</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
    transition: opacity .5s;
}

.fade-enter,
.fade-leave-to
/* .fade-leave-active below version 2.1.8 */

    {
    opacity: 0;
}
</style>
