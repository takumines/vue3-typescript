<script setup lang="ts">
import {computed, ref} from 'vue'
import CardList from './components/CardList.vue';
import SecondCardList from './components/SecondCardList.vue';

const isActiveTabName = ref(1)
const updateTab = (isFirst: number) => {
  isActiveTabName.value = isFirst
}

const currentComponent: ComponentDefinition = computed(() => {
  switch (isActiveTabName.value) {
    case 1:
      return CardList
    case 2:
      return SecondCardList
  }
});

</script>

<template>
  <div class="tab-changer">
    <button @click="updateTab( 1)">Tab 1</button>
    <button @click="updateTab(2)">Tab 2</button>
  </div>
  <div class="tab-contents">
<!--    <CardList></CardList>-->
    <component :is="currentComponent"></component>
<!--    <CardList v-if="isFirstTab"></CardList>-->
<!--    <SecondCardList v-if="!isFirstTab"></SecondCardList>-->
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.tab-contents {
  margin-top: 20px;

}
</style>
