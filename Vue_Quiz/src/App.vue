<template>
  <div id="app">
    <Title
      :noCorrect="noCorrect"
      :noTotal="noTotal"/>
   <Body 
   v-if="questions.length"
   :question="questions[index]"
   :next="next"
   :increment="increment"
   />
  </div>
</template>

<script>
import Title from './components/Title.vue'
import Body from './components/Body.vue'
export default {
  name: 'app',
  components: {
    Title,
    Body
  },
  data(){
   return{
     questions:[],
     index:0,
     noCorrect:0,
     noTotal:0
   }
  },
  methods:{
  next(){
    this.index++
  },
  increment(isCorrect){
    if(isCorrect)
    this.noCorrect++
    this.noTotal++
  }
  },
  mounted:function(){
    fetch('https://opentdb.com/api.php?amount=10',{
      method:'get'
    }).then((response)=>{
     return response.json()
    })
    .then(res=>{
      this.questions=res.results
    })
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
