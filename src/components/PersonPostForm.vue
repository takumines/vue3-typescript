<script setup lang="ts">
import { Person } from '../types/person';
import {computed, ref} from "vue";

let registerState: 'ok' | 'ng' = 'ng'

const inputName = ref<string>('')
const inputAge = ref<number>(0);
const emit = defineEmits(['register'])
const register = () => {
  const person: Person = {
    id: Math.random(),
    name: inputName.value,
    age: inputAge.value
  }
  emit('register', person)
  inputName.value = ''
  inputAge.value = 0
}
const nameLengthLimit = 15
const ageLimit = 0
const isValidName = computed(() => {
  return inputName.value.length < nameLengthLimit
});
const isValidAge = computed(() => {
  return inputAge.value >= ageLimit
})

</script>

<template>
 <div class="form-container">
   <div class="input-container">
     <div class="input-column">
       <span>name: </span>
       <input :class="{ 'input-error': !isValidName }" v-model="inputName" type="text">
     </div>
     <span class="error-message" v-if="!isValidName">{{ nameLengthLimit }} characters or less, please</span>
     <div class="input-column">
       <span>age: </span>
       <input :class="{ 'input-error': !isValidAge }" v-model="inputAge" type="number">
     </div>
     <span class="error-message" v-if="!isValidAge">{{ ageLimit }} number or less, please</span>
   </div>
   <button :disabled="(!isValidName || !isValidAge)" @click="register" class="register-button">register</button>
 </div>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(255, 241, 226);
  padding: 24px 0;
  width: 50%;
  margin-bottom: 12px;
  border-radius: 4px;
}

span {
  font-size: 18px;
  font-weight: bold;
}
.input-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 50px;
  margin-bottom: 20px;
}

.input-column {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

.input-error {
  background-color: rgb(244, 194, 190);
}

.error-message {
  font-size: 12px;
  color: rgb(244, 194, 190);
}

input {
  width: 120px;
  margin-bottom: 8px;
}

.register-button {
  margin-top: 10px;
}
</style>