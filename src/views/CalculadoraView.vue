<template>
  <div class="container text-center">
    <p>Calculadora sencilla</p>
    <p>{{ display }}</p>
    <div class="row">
      <div class="col">
        <button @click="reset" type="button" class="btn btn-success largo">Reset</button>
      </div>
      <div class="col">
        <button @click="deleteLast" type="button" class="btn btn-success largo">Delete</button>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <button @click="append('9')" type="button" class="btn btn-success largo">9</button>
      </div>
      <div class="col">
        <button @click="append('8')" type="button" class="btn btn-success largo">8</button>
      </div>
      <div class="col">
        <button @click="append('7')" type="button" class="btn btn-success largo">7</button>
      </div>
      <div class="col">
        <button @click="append('+')" type="button" class="btn btn-success largo">+</button>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <button @click="append('6')" type="button" class="btn btn-success largo">6</button>
      </div>
      <div class="col">
        <button @click="append('5')" type="button" class="btn btn-success largo">5</button>
      </div>
      <div class="col">
        <button @click="append('4')" type="button" class="btn btn-success largo">4</button>
      </div>
      <div class="col">
        <button @click="append('-')" type="button" class="btn btn-success largo">-</button>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <button @click="append('3')" type="button" class="btn btn-success largo">3</button>
      </div>
      <div class="col">
        <button @click="append('2')" type="button" class="btn btn-success largo">2</button>
      </div>
      <div class="col">
        <button @click="append('1')" type="button" class="btn btn-success largo">1</button>
      </div>
      <div class="col">
        <button @click="append('*')" type="button" class="btn btn-success largo">X</button>
      </div>
    </div>
    <div class="row">
      <div class="col">
        <button @click="calculate" type="button" class="btn btn-success largo">=</button>
      </div>
      <div class="col">
        <button @click="append('0')" type="button" class="btn btn-success largo">0</button>
      </div>
      <div class="col">
        <button @click="toggleSign" type="button" class="btn btn-success largo">-/+</button>
      </div>
      <div class="col">
        <button @click="append('/')" type="button" class="btn btn-success largo">/</button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const display = ref('');
const resetNext = ref(false);

const reset = () => {
  display.value = '';
  resetNext.value = false;
};

const deleteLast = () => {
  display.value = display.value.slice(0, -1);
  resetNext.value = false;
};

const append = (character: string) => {
  if (resetNext.value) {
    display.value = '';
    resetNext.value = false;
  }
  display.value += character;
};

const toggleSign = () => {
  if (display.value.startsWith('-')) {
    display.value = display.value.slice(1);
  } else {
    display.value = '-' + display.value;
  }
  resetNext.value = false;
};

const calculate = () => {
  try {
    display.value = eval(display.value).toString();
  } catch {
    display.value = 'Error';
  }
  resetNext.value = true;
};
</script>

<style scoped>
.largo {
  width: 90%;
  padding: 20px;
  margin: 10px;
}
</style>