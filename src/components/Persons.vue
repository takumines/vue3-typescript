<script setup lang="ts">
import PersonPostForm from './PersonPostForm.vue';
import PersonList from './PersonList.vue';
import { Person } from "../types/person";
import { ref, Ref } from "vue";

const persons = ref<Person[]>([])
const registerPerson = (person: Person) => {
  persons.value.push(person)
}
const deletePerson = (id: number) => {
  persons.value = persons.value.filter(person => person.id !== id)
}

</script>

<template>
  <div class="container">
    <h1>Title</h1>
    <PersonPostForm @register="registerPerson"/>
    <div class="list-container">
      <ul>
        <PersonList :persons="persons" @delete="deletePerson"/>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>