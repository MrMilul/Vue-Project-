<template>
  <div>
    <Header 
    :index="this.index"
    :TotalAnswer ="this.TotalAnswer"
    :CorrectAnswerNum ="this.CorrectAnswerNum"

    />
    <b-container class="bv-example-row" >

      <b-row sm="6" offset="6">
        <b-col><Content 
        :cQuestion='questionlist[index]' 
        :next = "next" 
        :increment = "this.increment"
        /></b-col>
      </b-row>

    </b-container>
    
  </div>
</template>

<script>
import Header from './components/Header'
import Content from './components/Content'

export default {
  name: 'App',
  components: {
    Header,
    Content
  }, 
  data() {
      return{
        cQuestion:[],
        questionlist:[], 
        index:0,
        TotalAnswer: 0,
        CorrectAnswerNum: 0,
      }
  },
  methods:{
    next(){
      if(this.index < 9){
        this.index ++
      }
      
    }, 
    increment(is_correct){
      if(is_correct){
        this.CorrectAnswerNum++
      }
      this.TotalAnswer++
    }
  },
  mounted: function (){
    fetch("https://opentdb.com/api.php?amount=10&category=11&difficulty=easy&type=multiple", {method: "get"})
    .then(
      (response)=>{
        return response.json()})
    .then((result)=>{
      return this.questionlist = result.results;
    })
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
