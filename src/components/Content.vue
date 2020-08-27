<template>
<div class="mt-1">
     <b-jumbotron>
          <template>{{cQuestion.question}}</template>

          <hr class="my-4">

          <b-list-group>
               <b-list-group-item  :class ="[ !Answered && Cindex === i ? 'selected': 
                    Answered && i ===  correctAnswer ? 'correct' : 
                     Answered && i !==  correctAnswer && i === Cindex? 'incorrect' : ''
                    ]" 
                    
               class='mb-2' 
               v-for="(answer,i) in ShuffledAnswers" :key="i"
               @click="SaveIndex(i)">
               {{answer}}
               </b-list-group-item>
          </b-list-group>

          <b-button class='mx-2' variant="primary" href="#"
          :disabled="Cindex === null || Answered" 
          @click="submitAnswers()">
     
          Submit
          </b-button>

          <b-button variant="success" href="#" @click='next()'>Next</b-button>

     </b-jumbotron>
</div>
</template>

<script>
import _ from 'lodash';

export default {
     props:{
          cQuestion: Object,
          next: Function,
          increment: Function,
         
          },
          data(){
               return{
                    Cindex : null,
                    ShuffledAnswers: [],
                    correctAnswer: null,
                    Answered: false,
               }           
          },
          watch:{
               cQuestion:{
                    immediate(){true},
                    handler(){
                    this.Cindex = null;
                    this.Answered=false,
                    this.correctAnswer=null,
                    this.ShuffleAnswers()
                    }
               }
               
          },
          methods:{
               SaveIndex(i){
                    this.Cindex = i
               },
               ShuffleAnswers(){
                     let answers = [...this.cQuestion.incorrect_answers,this.cQuestion.correct_answer]; 
                     this.ShuffledAnswers = _.shuffle(answers)
                     this.correctAnswer = this.ShuffledAnswers.indexOf(this.cQuestion.correct_answer)

               },
               submitAnswers(){
                   let is_correct = false; 
                   if(this.Cindex === this.correctAnswer){
                        is_correct = true;
                   }
                   this.Answered = true;
                    this.increment(is_correct)

               } 

          },
          computed: {
            answers(){
                 let answers = [...this.cQuestion.incorrect_answers]
                 answers.push(this.cQuestion.correct_answer)
                 return answers
            },   
          },
}
</script>

<style scoped>
.list-group-item:hover{
     background-color: rgba(211, 211, 236, 0.781);
     cursor: pointer;
}
.list-group-item:active{
     scale: 1.01;
}
.selected{
     background-color: rgba(119, 119, 252, 0.671);
}
.correct{
     background-color:greenyellow;
}
.incorrect{
      background-color: red;
}
</style>