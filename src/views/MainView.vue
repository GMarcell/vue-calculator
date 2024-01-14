<script setup lang="ts">
import { ref } from "vue";
const display = ref("0");

const handleBackSpace = (isBackSpace: boolean) => {
  if (isBackSpace) {
    if (display.value.length > 1) {
      display.value = display.value.substring(0, display.value.length - 1);
    } else {
      display.value = "0";
    }
  } else {
    display.value = "0";
  }
};

const handleButtonClick = (value: string | number) => {
  if (value == ".") {
    display.value = display.value + value;
  } else {
    if (display.value == "0") {
      display.value = String(value);
    } else {
      display.value = display.value + value;
    }
  }
};

const handleEqual = () => {
  if (display.value.includes("/")) {
    // ini distribution
    const arrayProblem = display.value.split("/");
    display.value = String(
      (Number(arrayProblem[0]) / Number(arrayProblem[1])).toFixed(2)
    );
  } else if (display.value.includes("*")) {
    // ini multiply
    const arrayProblem = display.value.split("*");
    display.value = String(
      (Number(arrayProblem[0]) * Number(arrayProblem[1])).toFixed(2)
    );
  } else if (display.value.includes("+")) {
    // ini plus
    const arrayProblem = display.value.split("+");
    display.value = String(
      (Number(arrayProblem[0]) + Number(arrayProblem[1])).toFixed(2)
    );
  } else {
    // ini minus
    const arrayProblem = display.value.split("-");
    display.value = String(
      (Number(arrayProblem[0]) - Number(arrayProblem[1])).toFixed(2)
    );
  }
};
</script>

<template>
  <div class="flex justify-center items-center">
    <div class="grid grid-cols-4 grid-rows-5 gap-2">
      <div
        class="h-24 flex justify-end items-center text-4xl col-span-4 p-4 border-2"
      >
        {{ display }}
      </div>
      <div
        class="w-24 h-24 bg-gray-500 flex justify-center items-center text-2xl rounded font-bold text-black"
        @click="handleBackSpace(true)"
      >
        ->
      </div>
      <div
        class="w-24 h-24 bg-gray-500 flex justify-center items-center text-2xl rounded font-bold text-black"
        @click="handleBackSpace(false)"
      >
        Del
      </div>
      <div
        class="w-24 h-24 bg-gray-500 flex justify-center items-center text-2xl rounded font-bold text-black"
        @click="handleButtonClick('%')"
      >
        %
      </div>
      <div
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('/')"
      >
        /
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(7)"
      >
        7
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(8)"
      >
        8
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(9)"
      >
        9
      </div>
      <div
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('*')"
      >
        *
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(4)"
      >
        4
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(5)"
      >
        5
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(6)"
      >
        6
      </div>
      <div
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('-')"
      >
        -
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(1)"
      >
        1
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(2)"
      >
        2
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(3)"
      >
        3
      </div>
      <div
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('+')"
      >
        +
      </div>
      <div
        class="h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold col-span-2"
        @click="handleButtonClick(0)"
      >
        0
      </div>
      <div
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('.')"
      >
        .
      </div>
      <div
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleEqual()"
      >
        =
      </div>
    </div>
  </div>
</template>
