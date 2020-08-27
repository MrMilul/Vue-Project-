<template>
     <div>
     <b-navbar toggleable="lg" type="dark" variant="dark">
          <b-navbar-brand href="#">
          <div class="h2 mb-0">
          <b-icon id='b-icon' icon="question-square"></b-icon>
          </div>
          </b-navbar-brand>
          <b-navbar-brand href="#">Question & Answer</b-navbar-brand>

          

          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

          <b-collapse id="nav-collapse" is-nav>
               <b-navbar-nav >
                    <b-nav-item href="#" >
                         Question Number: {{index +1 }} &nbsp;|
                         Correct Answers:{{CorrectAnswerNum}}/{{TotalAnswer}}
                         </b-nav-item>
               </b-navbar-nav>
          </b-collapse>
     </b-navbar>
</div>
</template>

<script>
export default {
     props:{
          index: Number,
          CorrectAnswerNum: Number,
          TotalAnswer:Number,
      }
       }
</script>

<style scoped>
    #b-icon{
          color: #7952b3;
     }
     #b-icon:hover{
          scale: 1.2;
     }
</style>