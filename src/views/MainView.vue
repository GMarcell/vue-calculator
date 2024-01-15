<script setup lang="ts">
import { split } from "postcss/lib/list";
import { ref } from "vue";
const display = ref("0");
const operatorCount = ref(0);

const operators = [
  ["*", (a: number, b: number) => +a * +b],
  ["/", (a: number, b: number) => +a / +b],
  ["+", (a: number, b: number) => +a + +b],
  ["-", (a: number, b: number) => +a - +b],
];

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

const handleButtonClick = (value: string | number, isOperator?: boolean) => {
  if (isOperator) {
    operatorCount.value = Number(operatorCount.value) + 1;
  }
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
  const split = [...display.value].reduce(
    (prev: any, current: any) =>
      Number.isInteger(+current) && Number.isInteger(+prev[prev.length - 1])
        ? [...prev.slice(0, -1), prev[prev.length - 1] + current]
        : [...prev, current],
    [""]
  );
  operators.forEach(([operator, funct]) => {
    for (let i = 1; i < split.length - 1; i++) {
      if (split[i] === operator) {
        // @ts-ignore
        split[i - 1] = funct(Number(split[i - 1]), Number(split[i + 1]));
        split.splice(i, 2);
        i--;
      }
    }
  });
  display.value = String(split);
  // for (let i = 0; i < operatorCount.value; i++) {
  //   if (display.value.includes("/")) {
  //     // ini distribution
  //     const arrayProblem = display.value.split("/");
  //     console.log(arrayProblem);
  //     display.value = String(
  //       (Number(arrayProblem[0]) / Number(arrayProblem[1])).toFixed(2)
  //     );
  //   } else if (display.value.includes("*")) {
  //     // ini multiply
  //     const arrayProblem = display.value.split("*");
  //     display.value = String(
  //       (Number(arrayProblem[0]) * Number(arrayProblem[1])).toFixed(2)
  //     );
  //   } else if (display.value.includes("+")) {
  //     // ini plus
  //     const arrayProblem = display.value.split("+");
  //     display.value = String(
  //       (Number(arrayProblem[0]) + Number(arrayProblem[1])).toFixed(2)
  //     );
  //   } else {
  //     // ini minus
  //     const arrayProblem = display.value.split("-");
  //     display.value = String(
  //       (Number(arrayProblem[0]) - Number(arrayProblem[1])).toFixed(2)
  //     );
  //   }
  // }
};

const handlePercent = () => {
  display.value = String(Number(display.value) / 100);
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
      <button
        class="w-24 h-24 bg-gray-500 flex justify-center items-center text-2xl rounded font-bold text-black"
        @click="handleBackSpace(true)"
      >
        ->
      </button>
      <button
        class="w-24 h-24 bg-gray-500 flex justify-center items-center text-2xl rounded font-bold text-black"
        @click="handleBackSpace(false)"
      >
        Del
      </button>
      <button
        class="w-24 h-24 bg-gray-500 flex justify-center items-center text-2xl rounded font-bold text-black"
        @click="handlePercent()"
      >
        %
      </button>
      <button
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('/', true)"
        :disabled="
          display[display.length - 1] == '/' ||
          display[display.length - 1] == '*' ||
          display[display.length - 1] == '+' ||
          display[display.length - 1] == '-' ||
          display == '0'
        "
      >
        /
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(7)"
      >
        7
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(8)"
      >
        8
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(9)"
      >
        9
      </button>
      <button
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('*', true)"
        :disabled="
          display[display.length - 1] == '/' ||
          display[display.length - 1] == '*' ||
          display[display.length - 1] == '+' ||
          display[display.length - 1] == '-' ||
          display == '0'
        "
      >
        *
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(4)"
      >
        4
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(5)"
      >
        5
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(6)"
      >
        6
      </button>
      <button
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('-', true)"
        :disabled="
          display[display.length - 1] == '/' ||
          display[display.length - 1] == '*' ||
          display[display.length - 1] == '+' ||
          display[display.length - 1] == '-' ||
          display == '0'
        "
      >
        -
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(1)"
      >
        1
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(2)"
      >
        2
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick(3)"
      >
        3
      </button>
      <button
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('+', true)"
        :disabled="
          display[display.length - 1] == '/' ||
          display[display.length - 1] == '*' ||
          display[display.length - 1] == '+' ||
          display[display.length - 1] == '-' ||
          display == '0'
        "
      >
        +
      </button>
      <button
        class="h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold col-span-2"
        @click="handleButtonClick(0)"
      >
        0
      </button>
      <button
        class="w-24 h-24 bg-gray-700 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleButtonClick('.')"
      >
        .
      </button>
      <button
        class="w-24 h-24 bg-yellow-600 flex justify-center items-center text-2xl rounded font-bold"
        @click="handleEqual()"
        :disabled="
          display[display.length - 1] == '/' ||
          display[display.length - 1] == '*' ||
          display[display.length - 1] == '+' ||
          display[display.length - 1] == '-' ||
          display == '0'
        "
      >
        =
      </button>
    </div>
  </div>
</template>
