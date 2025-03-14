<template>
  <div class="d-flex justify-content-center">
    <div>
      <div class="input-group">
        <button @click="decrement" class="btn btn-outline-secondary" type="button">-</button>
        <input type="number" v-model.number="value" class="form-control text-center">
        <button @click="increment" class="btn btn-outline-secondary" type="button">+</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  modelValue: {
    type: Number,
    required: true
  }
});

const emits = defineEmits(['update:modelValue']);

const value = ref(props.modelValue);

const increment = () => {
  value.value++;
};

const decrement = () => {
  if (value.value > 0) {
    value.value--;
  }
};

watch(value, (newValue) => {
  emits('update:modelValue', newValue);
});
</script>

<style scoped>
.input-group {
  display: flex;
  align-items: center;
  width: 150px;
}
/* Chrome, Safari, Edge, Opera */
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

/* Firefox */
input[type="number"] {
    -moz-appearance: textfield;
}
</style>
