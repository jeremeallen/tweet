<template>
  <div class="w-75 center ba b--black-10" id="twitterVue">
    <div class="pv2 tc bb b--black-10">
      <h1 class="ma0 f5 normal">Compose New Tweet</h1>
    </div>
    <div class="bg-near-white pa3">
      <textarea placeholder="Write your tweet here" name="tweet" v-model="tweet" rows="3" class="w-100 br2 ba b--black-10 pa2"></textarea>
      <div v-if="photoHasBeenUploaded" class="bg-black-10 pa2 flex">
        <figure class="mv0 ml0 mr3 relative flex items-center justify-center" v-for="(photo, $index) in photos">
        <button @click="removePhoto($index)" class="button-reset pointer dim bn bg-black h2 w2 br-100 white flex items-center justify-center absolute absolute--fill-l center">
          <i class="material-icons f5">close</i>
        </button>
        <img :src="photo" class="h3 w3" alt="Uploaded photo">
      </figure>
      </div>
      <input multiple @change="handlePhotoUpload" ref="photoUpload" type="file" class="hide">
      <div class="mt3 flex justify-between">
        <div>
          <button @click="triggerFileUpload" class="button-reset flex items-center br2 bn bg-transparent blue hover-bg-black-10 pointer">
            <i class="material-icons f3">photo_camera</i>
          </button>
        </div>
        <div class="flex items-center">
          <span class="mr3 black-70" v-bind:class="{ 'dark-red': underTwentyMark, 'light-red': underTenMark }">{{ charactersRemaining }}</span>
          <button :disabled="tweetIsOutOfRange" class="button-reset bg-blue bn white f6 fw5 pv2 ph3 br2 dim">Tweet</button>
        </div>
      </div>  
    </div>
  </div>
</template>

<script>
const MAX_TWEET_LENGTH = 140;

export default {
  name: 'tweet',
  data() {
    return {
      tweet: '',
      photos: [],
    };
  },
  computed: {
    tweetIsEmpty() {
      return this.tweet.length === 0;
    },
    charactersRemaining() {
      return MAX_TWEET_LENGTH - this.tweet.length;
    },
    tweetIsOutOfRange() {
      return this.charactersRemaining === MAX_TWEET_LENGTH || this.charactersRemaining < 0;
    },
    underTwentyMark() {
      return this.charactersRemaining <= 20 && this.charactersRemaining > 10;
    },
    underTenMark() {
      return this.charactersRemaining <= 10;
    },
    photoHasBeenUploaded() {
      return this.photos.length > 0;
    },
  },
  methods: {
    triggerFileUpload() {
      this.$refs.photoUpload.click(); // LOLWUT?
    },
    handlePhotoUpload(e) {
      const self = this;
      const files = e.target.files;

      for (let i = 0; i < files.length; i += 1) {
        const reader = new FileReader();
        reader.onloadend = (evt) => {
          self.photos.push(evt.target.result);
        };
        reader.readAsDataURL(files[i]);
      }
    },
    removePhoto(index) {
      this.photos.splice(index, 1);
    },
  },
};
</script>
<style lang='scss'>
  @import url(https://fonts.googleapis.com/icon?family=Material+Icons);

  button[disabled] {
    cursor: not-allowed;
    opacity: .5;
  }

  .hide {
    clip: rect(1px, 1px, 1px, 1px);
    height: 1px;
    overflow: hidden;
    position: absolute !important;
    width: 1px;
  }
</style>
