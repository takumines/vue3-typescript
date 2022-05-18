<script setup lang="ts">
import { Person } from "../types/person";

type Props = {
  persons: Person[]
}

const props = defineProps<Props>()
const emit = defineEmits(['delete'])
const onClickDelete = (id: number) => {
  emit('delete', id)
}
</script>

<template>
  <li v-for="person in props.persons" :key="person.id" class="person-list">
    <span>{{ person.name }}</span>
    <span>{{ person.age }}</span>
    <button @click="onClickDelete(person.id)">
      <span>delete</span>
    </button>
  </li>
</template>

<style scoped>
.person-list {
  list-style: none;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 20px;
  display: flex;
  font-weight: bold;
  justify-content: space-between;
  background-color: rgb(228, 201, 133);
  padding: 8px 20px;
  width: 300px;
}
</style>