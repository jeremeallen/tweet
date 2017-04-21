<template>
  <div class="w-75 center ba b--black-10" id="twitterVue">
    <div class="pv2 tc bb b--black-10">
      <h1 class="ma0 f5 normal">Compose New Tweet</h1>
    </div>
    <div class="bg-near-white pa3">
      <textarea placeholder="Write your tweet here" name="tweet" v-model="tweet" rows="3" class="w-100 br2 ba b--black-10 pa2"></textarea>
      <div class="mt3 tr">
        <button :disabled="tweetIsEmpty" class="button-reset bg-blue bn white f6 fw5 pv2 ph3 br2 dim">Tweet</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
