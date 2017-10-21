<template>
  <div id="app">
    <div class="container">
      <div class="row">
          <div class="col-sm-12 col-md-6 col-lg-4 card" v-for="(person,index) in this.data"  >
       <transition-group appear
        class="transition" 
        name="custom-classes-transition" 
        mode="in-out"
        enter-active-class="animated fadeInUp"
       >
        <div class="wrapper" :key="index" v-show="apear">
          <span class="available":class='{hidden:getRandom(0,1)}'>
            available
          </span><span class="price">{{`$${getRandom(30,40)}/hr`}}</span>
          <div class="img"><img :src="person.picture.large" :alt="customAlt[index]"></div>
          <h2>{{toUpperFirstChar[index]}}</h2>
          <span class="type">{{randomType}}</span>
          <span class="spec">{{workType}}</span>
          <div class="inner">
            <span class="technology" v-for="technology in technologies">{{technology}}</span>
          </div>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Et, quos.</p>
          <hr>
          <a href="#" @click.prevent="wtf">VIEW PROFILE</a>
           </div>
       </transition-group>
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
      name:null,
      type:['Front-end developer','UI/UX designer','Interactive designer'],
      workType:'Freelancer',
      technologies:['PHP','Android','iOS'],
      errors:[],
      text:'text',
      apear:true
    }
   },created(){
        axios.get('https://randomuser.me/api/?results=10&inc=name,gender,picture,nat&nat=us,ca,gb&noinfo')
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
      
   },computed:{
       toUpperFirstChar(){
        return this.data.map(function(elem) {
        var firtsName = elem.name.first;
        var secondName = elem.name.last;
        return firtsName.charAt(0).toUpperCase()+firtsName.slice(1)+" "+
               secondName.charAt(0).toUpperCase()+ secondName.slice(1);
        });
      },
      randomType(){
        var rndNumber = this.getRandom(0,2);
        return this.type[rndNumber];
      },
      customAlt(){
        return this.data.map(function(elem) {
          var firtsName = elem.name.first;
          var secondName = elem.name.last;
          return `On picture is ${firtsName} ${secondName}`;
        })
      }
   }
}
</script>

<style lang="scss">
@import './assets/scss/main.scss'
</style>
