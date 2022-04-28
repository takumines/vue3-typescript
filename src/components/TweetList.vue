<script setup lang="ts">
import { defineProps, defineEmits } from "vue";
import {Tweet} from "../types/tweet.";

type Props = {
  tweets: Tweet[]
}

defineProps<Props>()
const emit = defineEmits(['delete-tweet'])
const deleteTweet = (id: number) => {
  emit('delete-tweet', id)
}
</script>

<template>
  <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
    <span>{{ tweet.description }}</span>
    <button class="delete-button" @click="deleteTweet(tweet.id)">delete</button>
  </li>
</template>

<style scoped>
.tweet-list {
  list-style: none;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 12px;
  display: flex;
  justify-content: space-between;
  background-color: rgb(204, 219, 233);
  padding: 8px 20px;
  width: 300px;
  align-items: center;
}

.delete-button {
  color: #fff;
  font-weight: bold;
  background-color: #c99a68;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 22px;
}

.delete-button:hover {
  background-color: #ac783f;
}
</style>