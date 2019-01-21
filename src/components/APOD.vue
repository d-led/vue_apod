<template>
  <div class="apod">
    <h1>Choose the date:</h1>
    <label>{{Date.now()}}</label></br>
    <button @click="loadApod">Go!</button>
    <h1>{{apod.title}}</h1>
    <img v-if="apod.url" v-bind:src="apod.url">
    <p v-if="apod.explanation">{{apod.explanation}}</p>  
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component({
  props: {
      apiKey: String // todo
  }
})
export default class HelloWorld extends Vue {
  apod = {
    title: '',
    url: '',
    explanation: ''
  }
  
  loadApod() {
    var vm = this
    fetch("https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY")
    .then(function (response) {
    return response.json()
    })
    .then(function (data) {
      vm.apod = data
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
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
