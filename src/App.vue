<template>
  <div id="app">
    <div class="columns is-mobile">
      <div class="column is-8 is-offset-2">
        <input v-model="branch" class="input" type="text" placeholder="branch">
      </div>
    </div>
    <div class="columns is-mobile">
      <div class="column is-8 is-offset-2">
        <input v-model="review" class="input" type="text" placeholder="review">
      </div>
    </div>
    <div class="columns is-mobile">
      <div class="column is-8 is-offset-2">
        <textarea v-model="result" class="textarea" readonly placeholder="script" rows="20"></textarea>
        <div class="column"><a v-on:click="setScript" class="button is-success">Generate</a></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: function() {
    return {
      branch: '',
      review: '',
      script: 'git checkout dev  &&\ngit pull &&\ngit merge  <branch> --no-ff -m " <review> merge  <branch> into dev" &&\ngit push origin dev &&\ngit checkout qa &&\ngit pull &&\ngit merge  <branch> --no-ff -m " <review> merge  <branch> into qa" &&\ngit push origin qa &&\ngit checkout master  &&\ngit pull &&\ngit merge  <branch> --no-ff -m " <review> merge  <branch> into master" &&\ngit push origin master',
      result: ''
    }
  },
  methods: {
    getBranch: function() {
      this.result = this.result.replace(new RegExp('<branch>', 'g'), this.branch)
    },
    getReview: function() {
      this.result = this.result.replace(new RegExp('<review>', 'g'), this.review)
    },
    setScript: function() {
      this.result = this.script
      this.getBranch()
      this.getReview()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
