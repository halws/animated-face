<template>
  <div id="app">
    <h1>Hello</h1>
   <!--  <pre>
      {{this.data}}
    </pre> -->
    <pre v-for="person in this.data">{{person}} <hr><br> </pre>
    <div class="container">
      <div class="row">
        <div 
          class="col-sm-12 col-md-4 col-lg-3 card" 
          v-for="person in this.data">
        <div class="img"><img :src="person.picture.large" alt=""></div>
        <h2>{{person.name.first}} {{person.name.last}}</h2>
        <span class="type">{{randomType()}}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from './../node_modules/axios/dist/axios.min.js';
export default {
 data(){
  return{
    data:null,
    type:['Front-end developer','UI/UX designer','Interactive designer'],
    workType:'Freelancer',
    technology:['PHP','Android','iOS'],
    errors:[]
  }
 },created(){
    axios.get('https://randomuser.me/api/?results=2&inc=name,gender,picture,nat&nat=gb,us,ca&noinfo')
    .then(response=>{
      this.data = response.data.results;
  })
  .catch(e=>{
    this.errors.push(e);
  })
 },
 methods:{
  getRandom(min,max){
     return Math.floor(Math.random()*(max-min+1)+min);
  },
  randomType(){
    var rndNumber = this.getRandom(0,2);
    return this.type[rndNumber];
  }
 }
}
</script>

<style lang="scss">
@import './assets/scss/main.scss';
</style>
