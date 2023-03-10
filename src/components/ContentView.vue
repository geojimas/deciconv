<template>
  <div class="flex h-screen justify-evenly items-center flex-wrap">
    <div class="animate__animated animate__fadeInDown flex items-center justify-center px-5">
      <div class="rounded-lg bg-white shadow-lg text-gray-800">
        <div class="flex items-center flex-col p-5">
          <h2 class="text-xl font-bold text-black shadow-xl text-center px-5">Type a Number</h2>
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
        style="max-width: 400px"
        class="flex flex-wrap flex-col rounded-lg bg-white shadow-lg p-8 font-bold">
        <p class="text-2xl mb-4 font-bold text-black shadow-xl text-center px-5">Result</p>
        <div class="flex items-center mb-2">
          <p class="shadow-xl">
            Decimal :
            <span
              v-if="decimalNumber.toString().length > 10"
              class="text-2xl text-teal-500 ml-2 font-bold"
              >{{ decimalNumber.toString().substring(0, 10) }}...</span
            >
            <span
              v-else-if="decimalNumber.toString().length <= 10"
              class="text-2xl text-teal-500 ml-2 font-bold"
              >{{ decimalNumber }}</span
            >
          </p>
          <button
            v-if="decimalNumber > 0"
            v-clipboard:copy="decimalNumber"
            v-clipboard:success="onSuccess"
            v-clipboard:error="onError"
            class="text-md rounded-xl border-white p-2 ml-1 hover:bg-slate-100 active:translate-y-0.5 focus:outline-none focus:ring">
            <CopyIcon />
          </button>
        </div>
        <div class="flex items-center mb-2">
          <p class="shadow-xl">
            Binary :
            <span v-if="binaryNumber.length > 10" class="text-2xl text-pink-600 ml-2 font-bold"
              >{{ binaryNumber.substring(0, 10) }}...</span
            >
            <span
              v-else-if="binaryNumber.length <= 10"
              class="text-2xl text-pink-600 ml-2 font-bold"
              >{{ binaryNumber }}</span
            >
          </p>
          <button
            v-if="binaryNumber > 0"
            v-clipboard:copy="binaryNumber"
            v-clipboard:success="onSuccess"
            v-clipboard:error="onError"
            class="text-md rounded-xl border-white p-2 ml-1 hover:bg-slate-100 active:translate-y-0.5 focus:outline-none focus:ring">
            <CopyIcon />
          </button>
        </div>
        <div class="flex items-center mb-2">
          <p class="shadow-xl">
            Octal :
            <span v-if="octaNumber.length > 10" class="text-2xl text-pink-600 ml-2 font-bold"
              >{{ octaNumber.substring(0, 10) }}...</span
            >
            <span
              v-else-if="octaNumber.length <= 10"
              class="text-2xl text-pink-600 ml-2 font-bold"
              >{{ octaNumber }}</span
            >
          </p>
          <button
            v-if="octaNumber > 0"
            v-clipboard:copy="octaNumber"
            v-clipboard:success="onSuccess"
            v-clipboard:error="onError"
            class="text-md rounded-xl border-white p-2 ml-1 hover:bg-slate-100 active:translate-y-0.5 focus:outline-none focus:ring">
            <CopyIcon />
          </button>
        </div>
        <div class="flex items-center mb-2">
          <p class="shadow-xl">
            Hexadecimal :
            <span v-if="hexadecNumber.length > 10" class="text-2xl text-pink-600 ml-2 font-bold"
              >{{ hexadecNumber.substring(0, 10) }}...</span
            >
            <span
              v-else-if="hexadecNumber.length <= 10"
              class="text-2xl text-pink-600 ml-2 font-bold"
              >{{ hexadecNumber }}</span
            >
          </p>
          <button
            v-if="hexadecNumber.length > 0"
            v-clipboard:copy="hexadecNumber"
            v-clipboard:success="onSuccess"
            v-clipboard:error="onError"
            class="text-md rounded-xl border-white p-2 ml-1 hover:bg-slate-100 active:translate-y-0.5 focus:outline-none focus:ring">
            <CopyIcon />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import CopyIcon from './CopyIcon.vue'
import { notify } from '@kyvg/vue3-notification'

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

const onSuccess = () => {
  notify({
    title: 'Copied !',
    text: 'Copied to clipboard !',
    type: 'success',
    duration: 2000,
    speed: 500
  })
}
const onError = () => {
  notify({
    title: 'Error',
    text: "Didn't copy :( '",
    type: 'error',
    duration: 2000,
    speed: 500
  })
}
</script>
