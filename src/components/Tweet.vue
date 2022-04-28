<script setup lang="ts">
import { ref } from "vue";

interface Tweet {
  id: number,
  description: string
}

const inputDesc = ref<string>('')
const tweets = ref<Tweet[]>([])

const postTweet = () => {
  const tweet: Tweet = {
    id: tweets.value.length + 1,
    description: inputDesc.value
  }
  inputDesc.value = ''
  tweets.value.push(tweet)
}

const deleteTweet = (id: number) => {
  tweets.value = tweets.value.filter(tweet => tweet.id !== id)
}
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <div class="form-container">
      <input v-model="inputDesc">
      <button @click="postTweet" class="save-button">post</button>
    </div>
    <div class="tweet-container">
      <p v-if="tweets.length <= 0">No tweet have been added</p>
      <ul>
        <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
          <span>{{ tweet.description }}</span>
          <button class="delete-button" @click="deleteTweet(tweet.id)">delete</button>
        </li>
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

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: aliceblue;
  padding: 24px 0;
  width: 60%;
  margin-bottom: 12px;
  border-radius: 4px;
}

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
}

.save-button {
  color: #fff;
  font-weight: bold;
  background-color: #68c9c9;
  border-radius: 2px;
  border: none;
  width: 60px;
  height: 22px;
}

.save-button:hover {
  background-color: #37bdbd;
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

input {
  margin-bottom: 16px;
}
</style>