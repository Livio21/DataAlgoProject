<template>
  <div class="mx-auto my-5 flex flex-col gap-10 items-center max-w-6xl bg-gray-100 rounded-3xl p-10 ">
    <div class="">
      <h1 class="font-bold text-5xl pb-5 text-slate-800">Caesar Cipher</h1>
      <p class="">This is a simple Caesar Cipher app. It is a type of substitution cipher in which each
        letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet. For example,
        with a shift of 3, D would be replaced by A, E would become B, and so on. The method is named after Julius
        Caesar, who used it in his private correspondence.</p>
    </div>
    <label class="relative inline-flex items-center cursor-pointer">
      <input type="checkbox" value="true" class="sr-only peer" v-model="option">
      <div
        class="w-14 h-7 bg-gray-200 peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-blue-300  rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-0.5 after:left-[4px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-6 after:w-6 after:transition-all border-gray-600 peer-checked:bg-red-600">
      </div>
      <span class="ml-3 text-sm font-medium text-gray-900 ">{{ !option ? 'Decrypt?' : 'Encrypt?' }}</span>
    </label>
    <form @submit.prevent=""
      class="grid grid-cols-3 grid-rows-2 grid-flow-dense divide-x-2 rounded-3xl shadow-md bg-white ">
      <div class=" row-span-2 col-span-2">
        <textarea name="text" id="" rows="10"
          class="p-5 w-full h-full rounded-3xl rounded-r-none resize-none focus:outline-none text-lg"
          placeholder="Enter text here" v-model="text"></textarea>
      </div>
      <div class=" relative  row-span-1 col-span-1 min-h-full border-b-2 ">
        <input type="text" name="shift" id="shift" placeholder="Shift"
          class="text-center w-full h-full text-6xl  rounded-tr-3xl font-bold text-slate-600 max-w-fit focus:outline-none "
          min="0" v-model="shift">
        <div class="grid grid-flow-row h-full  font-bold text-2xl absolute right-0 top-0 ">
          <button class="p-4 hover:bg-gray-100" @click="shift++">+</button>
          <button class="p-4 hover:bg-gray-100" @click="shift == 0 ? shift = shift : shift--">-</button>
        </div>
      </div>
      <button
        class=" p-3 rounded-br-3xl text-slate-50 text-2xl font-semibold shadow-sm row-span-1 col-span-1 transition duration-100 ease-in-out "
        :class="option ? 'bg-red-500 active:bg-red-600 hover:bg-red-400' : 'bg-green-500 active:bg-green-600 hover:bg-green-400'"
        @click="btnAction">{{ option? 'Decrypt': 'Encrypt' }}</button>
    </form>

    <div class=" w-full flex flex-col gap-5">
      <h2 class="text-2xl font-bold text-slate-800 ">Result</h2>
      <p class="text-slate-600">Shift: {{ shift }}</p>
      <p class="bg-white rounded-3xl p-5 text-slate-600 font-semibold text-lg">{{ result? result: 'Result goes here' }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const text = ref('');
const shift = ref(0);
const result = ref('');
const option = ref(false);


const btnAction = () => {
  if (option.value == true) {
    if (result.value) result.value = ''
    decrypt()
  } else {
    if (result.value) result.value = ''
    encrypt()
  }
}

const encrypt = () => {
  // Wrap the shift.value
  if (shift.value < 0) {
    return encrypt(text.value, shift.value + 26);
  }

  // Go through each character
  for (var i = 0; i < text.value.length; i++) {
    // Get the character we'll be appending
    var c = text.value[i];

    // If it's a letter...
    if (c.match(/[a-z]/i)) {
      // Get its code
      var code = text.value.charCodeAt(i);

      // Uppercase letters
      if (code >= 65 && code <= 90) {
        c = String.fromCharCode(((code - 65 + shift.value) % 26) + 65);
      }

      // Lowercase letters
      else if (code >= 97 && code <= 122) {
        c = String.fromCharCode(((code - 97 + shift.value) % 26) + 97);
      }
    }

    // Append
    result.value += c;
  }

  // All done!
  return result.value;
};

//function to decrypt the text

const decrypt = () => {
  // Wrap the shift.value
  if (shift.value < 0) {
    return decrypt(text.value, shift.value + 26);
  }

  // Go through each character
  for (var i = 0; i < text.value.length; i++) {
    // Get the character we'll be appending
    var c = text.value[i];

    // If it's a letter...
    if (c.match(/[a-z]/i)) {
      // Get its code
      var code = text.value.charCodeAt(i);

      // Uppercase letters
      if (code >= 65 && code <= 90) {
        c = String.fromCharCode(((code - 65 - shift.value + 26) % 26) + 65);
      }

      // Lowercase letters
      else if (code >= 97 && code <= 122) {
        c = String.fromCharCode(((code - 97 - shift.value + 26) % 26) + 97);
      }
    }

    // Append
    result.value += c;
  }

  // All done!
  return result.value;
};




</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');

* {
  font-family: 'Roboto', sans-serif;
}
</style>