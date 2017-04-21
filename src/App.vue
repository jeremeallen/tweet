<template>
  <div id="app">
    <tweet></tweet>
  </div>
</template>

<script>
import Tweet from './components/Tweet';

export default {
  name: 'app',
  data() {
    return {};
  },
  computed: {
    tweetIsEmpty() {
      return this.tweet.length === 0;
    },
  },
  components: {
    Tweet,
  },
};
</script>

<style>
</style>
