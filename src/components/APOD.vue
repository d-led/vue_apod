<template>
  <div class="container text-left">
    <div class="row">
      <div class="col-2 mb-1">
        <div class="row">
          <h2>Choose the date</h2>
        </div>
        <div class="row">
          <datetime class="border mb-3 mt" type="date" v-model="dateString" :auto=true></datetime>
        </div>
        <div class="row">
          <b-btn @click="loadApod">Go!</b-btn>
           <div v-if="apod.msg" class="row alert alert-danger" role="alert">
            {{apod.msg}}
          </div>
        
        </div>

      </div>
      <div class="col mb-1">
        <div class="row">
          <h2>{{apod.title}}</h2>
        </div>
        <div class="row">
          <img v-if="apod.url && apod.media_type=='image'" v-bind:src="apod.url" height="auto" />
          <iframe :src="apod.url" frameborder="0" allowfullscreen></iframe>
        </div>
        <div class="row">
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
    explanation: '',
    media_type: 'image',
    msg: '',
  }

  dateString = Date.now().toString()

  get queryDate() {
    // debugger;
    let date = new Date(Date.now());
    if(typeof this.dateString!='undefined' && this.dateString) {
      date = new Date(this.dateString);
    }
    return DateTime.fromJSDate(date).toFormat('yyyy-MM-dd');
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
