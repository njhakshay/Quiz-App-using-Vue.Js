<template>
    <div>
  <marquee>  <h1>General Quiz</h1></marquee>
 <b-jumbotron>
   <template slot="lead">
     {{question.question}}
     </template>

     <hr class="my-4"/>
     <b-list-group >
  <b-list-group-item v-for="(answer,index) in answers" 
  :key="index" @click.prevent="checkanswer(index)"
   :class="answerClass(index)">
   {{shuffleanswer[index]}}
   </b-list-group-item>
</b-list-group>
    <b-button variant="primary" href="#" @click="submitanswer" 
    :disabled="(myIndex===null || answered) || counter>10"> Submit </b-button>
    <b-button @click="next" variant="primary" href="#" :disabled="answered===false || counter>9"> Next </b-button>
  </b-jumbotron>
    </div>
</template>
<script>
import _ from 'lodash'
export default {
props:{
  question : Object,
  next:Function,
  increment:Function
},
data(){
return{
  myIndex:null,
  correctIndex:null,
  shuffleanswer:[],
  answered:false,
  counter:0
}
},
methods:{
  checkanswer(index){
    this.myIndex=index
  },
  shuffleanswers(){
    let answer=[...this.question.incorrect_answers,this.question.correct_answer]
    this.shuffleanswer=_.shuffle(answer)
    this.correctIndex=this.shuffleanswer.indexOf(this.question.correct_answer)
  },
  submitanswer(){
    let isCorrect=false
    if(this.myIndex===this.correctIndex)
    {
      isCorrect=true
    }
    this.answered=true
    this.increment(isCorrect)
  },
  answerClass(index){
    let answerClass=''
    if(!this.answered && this.myIndex === index)
        answerClass='selected'
    else if(this.answered && this.correctIndex===index){
        answerClass='correct'
    }
    else if(this.answered && this.correctIndex!==index && this.myIndex===index)
        {answerClass='incorrect'
          }
    return answerClass
  }
},
mounted()
{
this.shuffleanswers()
},
watch:
{
  question:{
    immediate:true,
    handler(){
      this.myIndex=null
      this.shuffleanswers()
      this.answered=false
      this.counter++
    }
  }
},
  computed:{
   answers(){
 let answers=[...this.question.incorrect_answers]
 answers.push(this.question.correct_answer)
 return answers
   }
  }
}
</script>

<style scoped>
.list-group{
  margin-bottom:12px;
}
.btn{
  background-color: rgb(150, 142, 194);
  margin:0 5px;

}
.list-group-item:hover{
  background:rgb(233, 203, 203);
  cursor: pointer;
}
.selected{
  background:rgb(161, 161, 192)
}
.correct{
  background:green
}
.incorrect{
  background:red;
}
</style>



