
<template>
  <div id="app">
  <!-- Questions: display a div for each question -->
<!-- show only if the index of the quetion is equal to the question index -->
  <div v-for="(quiz, index) in quizez" v-show="index === questionindex" :key="index">
<!-- display the quiz Category -->
  <h1>{{ quiz.category }}</h1>
<!-- display the quiz question -->
  <h2>{{ quiz.question }}</h2>
  <!-- Responses: display a li for each possible response with a radio button -->
  <ol>
<!--display the quiz options -->
  <li v-for="answer in quiz.incorrect_answers" :key="answer">
  <label>
<!-- bind the options to the array index of the answers array that matches this index -->
  <input type="radio" name="answer" v-model="answers[index]" :value="answer"> {{answer}}
  </label>
  </li>
  </ol>

  </div>
  <!-- do not display if the question index exceeds the length of all quizez -->
  <div v-if="questionindex < quizez.length">
  <!-- display only if the question index is greater than zero -->
  <!-- onclick of this button, call the previous function, and show last question -->
  <button v-if="questionindex > 0" v-on:click="prev">
  prev
  </button>
 <!-- onclick of this button, call the next function, and show next question -->
  <button v-on:click="next">
  next
</button>
</div>
<!-- show total score, if the questions are completed -->
<span v-if="questionindex == quizez.length">Your Total score is {{score}} / {{quizez.length}}</span>

</div>
</template>

<script>
import * as data from './data.js';

export default {
  name: 'App',
  data : function (){
  return{
    questionindex:0,
    quizez:data.quiz_questions,
    answers:Array(data.quiz_questions.length).fill('')
   }
  },
  methods:{
    next(){
      this.questionindex++;
    },
    prev(){
      this.questionindex--;
    }
  },
  computed:{
    score(){
      var total = 0;
      for(var i=0; i< this.answers.length;i++){
          if(this.answers[i]==this.quizez[i].correct_answer){
            total+=1
          }
      }
      return total;
    }
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
