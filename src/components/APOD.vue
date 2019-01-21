<template>
  <div class="container text-left">
    <div class="row">
    <div class="col-2 mb-1">
      <div class="row">
    <h2>Choose the date</h2>
      </div>
      <div class="row">


    <datetime type="date" format="yyyy-MM-dd" v-model="dateString" auto=true></datetime>
    </div>
        <div class="row">
    <b-btn @click="loadApod">Go!</b-btn>
      </div>
      </div>
    <div class="col mb-1">
      <div class="row">
    <h2>{{apod.title}}</h2>
    <img v-if="apod.url" v-bind:src="apod.url" height="auto">
    <p v-if="apod.explanation">{{apod.explanation}}</p>
      </div>
    </div>
  </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import Datetime from 'vue-datetime';
import { DateTime } from 'luxon';
// You need a specific loader for CSS files
import 'vue-datetime/dist/vue-datetime.css';

Vue.component('datetime', Datetime);
Vue.use(Datetime)

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

  dateString = Date.now().toString()

  get queryDate() {
    let date = new Date(this.dateString);
    return DateTime.fromJSDate(date).toFormat('yyyy-MM-dd');
  }

  mounted () {
    this.dateString = Date.now().toString()
  }
  
  loadApod() {
    var vm = this
    fetch(`https://api.nasa.gov/planetary/apod?api_key=93Zc6xLbVySlaBhnVFbCRfhORrR71T47SYTu8JUf&date=${vm.queryDate}`)
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
