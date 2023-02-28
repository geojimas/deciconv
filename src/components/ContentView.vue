<template>
  <div class="mb-auto flex h-screen justify-evenly items-center flex-wrap">
    <div class="animate__animated animate__fadeInDown flex items-center justify-center px-5">
      <div
        class="rounded-lg bg-white shadow-lg text-gray-800"
        style="max-width: auto">
        <div class="flex items-center flex-col p-5">
          <h2 class="text-lg font-bold text-yellow-800 shadow-xl text-center px-5">Type a Number</h2>
          <input
            type="tel"
            name="number"
            @keypress="onlyNumber"
            v-model.number="decimalNumber"
            @input="calculateNumbers"
            class="shadow-xl text-xl p-1 m-4 text-black font-bold border-4 border-teal-500 rounded focus:outline-none" />
          <!-- <button
              type="button"
              @click="calculateNumbers"
              class="w-24 rounded group relative inline-block overflow-hidden border-2 border-red-400 p-2 focus:outline-none focus:ring">
              <span
                class="absolute inset-y-0 left-0 w-[2px] bg-red-400 transition-all group-hover:w-full group-active:bg-indigo-500"></span>

              <span
                class="relative text-sm font-medium text-red-400 transition-colors group-hover:text-white">
                Calculate
              </span>
            </button> -->
        </div>
      </div>
    </div>
    <div class="animate__animated animate__fadeInDown">
      <div
        class="rounded-lg bg-white shadow-lg p-8 text-gray-800"
        style="max-width: auto">
        <p class="text-lg mb-4 font-bold text-yellow-800 shadow-xl text-center px-5">
          Result
        </p>
        <h3 class="shadow-xl mb-4">
          Decimal :
          <span class="text-xl text-teal-500 font-bold">{{ decimalNumber }}</span>
        </h3>
        <h3 class="shadow-xl mb-4">
          Binary : <span class="text-xl text-red-500 font-bold">{{ binaryNumber }}</span>
        </h3>
        <h3 class="shadow-xl mb-4">
          Octal : <span class="text-xl text-red-500 font-bold">{{ octaNumber }}</span>
        </h3>
        <h3 class="shadow-xl">
          Hexadecimal : <span class="text-xl text-red-500 font-bold">{{ hexadecNumber }}</span>
        </h3>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

function onlyNumber($event) {
  // console.log($event.keyCode) // keyCodes value
  const keyCode = $event.keyCode ? $event.keyCode : $event.which
  if ((keyCode < 48 || keyCode > 57) && keyCode !== 46) {
    // 46 is dot
    $event.preventDefault()
  }
}

const binaryNumber = ref(0)
const decimalNumber = ref(0)
const octaNumber = ref(0)
const hexadecNumber = ref(0)

function calculateNumbers() {
  binaryNumber.value = decimalNumber.value.toString(2)
  octaNumber.value = decimalNumber.value.toString(8)
  hexadecNumber.value = decimalNumber.value.toString(16)
}
</script>
