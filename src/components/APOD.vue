<template>
  <div class="container text-left">
    <div class="row">
    <div class="col-2">
      <div class="row">
    <h2>Choose the date</h2>
      </div>
      <div class="row">


    <label>{{Date.now()}}</label>
    </div>
        <div class="row">
    <b-btn @click="loadApod">Go!</b-btn>
      </div>
      </div>
    <div class="col">
      <div class="row">
    <h2>{{apod.title}}</h2>
    <img v-if="apod.url" v-bind:src="apod.url" class="img-thumbnail" height="auto">
    <p v-if="apod.explanation">{{apod.explanation}}</p>
      </div>
    </div>
  </div>
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
    fetch("https://api.nasa.gov/planetary/apod?api_key=93Zc6xLbVySlaBhnVFbCRfhORrR71T47SYTu8JUf")
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
</style>
