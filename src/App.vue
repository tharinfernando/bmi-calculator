<template>
  <div class="bg-gray-200 min-h-screen flex flex-col items-center justify-center">
    <div class="bg-white rounded shadow p-4">
      <h1 class="text-2xl font-bold mb-4">BMI Calculator</h1>
      <div class="mb-4">
        <label for="name" class="font-semibold">Name</label>
        <input id="name" type="text" class="border border-gray-400 rounded px-2 py-1 ml-2" v-model="name">
      </div>
      <div class="mb-4">
        <label for="age" class="font-semibold">Age</label>
        <input id="age" type="number" class="border border-gray-400 rounded px-2 py-1 ml-2" v-model="age">
      </div>
      <div class="mb-4">
        <label for="weight" class="font-semibold">Weight (kg)</label>
        <input id="weight" type="number" class="border border-gray-400 rounded px-2 py-1 ml-2" v-model="weight">
      </div>
      <div class="mb-4">
        <label for="height" class="font-semibold">Height (cm)</label>
        <input id="height" type="number" class="border border-gray-400 rounded px-2 py-1 ml-2" v-model="height">
      </div>
      <div class="mb-4">
        <button class="bg-blue-500 text-white rounded px-4 py-2" @click="calculateBMI">Calculate BMI</button>
      </div>
      <div class="mb-4">
        <button class="bg-gray-500 text-white rounded px-4 py-2 ml-2" @click="clearInputs">Clear</button>
      </div>
      <div v-if="bmi !== null" class="mb-4">
        <p class="font-semibold">Your Name is {{ name }}</p>
        <p class="font-semibold">Your {{ ageStatus }}</p>
        <p class="font-semibold">Your BMI is {{ bmi.toFixed(2) }}</p>
        <p class="font-semibold">You are {{ bmiStatus }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: null,
      age: null,
      weight: null,
      height: null,
      bmi: null,
    };
  },
  computed: {
    bmiStatus() {
      if (this.bmi < 18.5) {
        return 'Underweight';
      } else if (this.bmi >= 18.5 && this.bmi < 25) {
        return 'Normal weight';
      } else if (this.bmi >= 25 && this.bmi < 30) {
        return 'Overweight';
      } else {
        return 'Obese';
      }
    },
    ageStatus() {
      if (this.age <= 18) {
        return 'a Teen';
      } else {
        return 'an Adult';
      }
    }
  },
  methods: {
    calculateBMI() {
      if (this.weight && this.height) {
        const heightInMeters = this.height / 100;
        this.bmi = this.weight / (heightInMeters * heightInMeters);
      }
    },
    clearInputs() {
      this.name = null;
      this.age = null;
      this.weight = null;
      this.height = null;
      this.bmi = null;
    },
  },
};
</script>
