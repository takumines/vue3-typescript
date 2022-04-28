<script setup lang="ts">
import { ref } from "vue";
import TweetPostForm from './TweetPostForm.vue';
import TweetList from "./TweetList.vue";
import { Tweet } from "../types/tweet.";

const tweets = ref<Tweet[]>([])
const postTweet = (description: string) => {
  const tweet: Tweet = {
    id: tweets.value.length + 1,
    description
  }
  tweets.value.push(tweet)
}

const deleteTweet = (id: number) => {
  tweets.value = tweets.value.filter(tweet => tweet.id !== id)
}
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <TweetPostForm @post-tweet="postTweet"/>
    <div class="tweet-container">
      <p v-if="tweets.length <= 0">No tweet have been added</p>
      <ul>
        <TweetList :tweets="tweets" @delete-tweet="deleteTweet"/>
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

input {
  margin-bottom: 16px;
}
</style>