<template>
  <div id="app">
    <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
      :totalQuestions="totalQuestions"
    />
    {{totalQuestions[0]}}

    <b-container class="bv-example-row">
      <b-row>
        <b-col xs="10" sm="10" offset-sm="1">
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import _ from 'lodash'

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      totalQuestions: 0
    }
  },
  methods: {
    next() {
      if (this.index !== this.questions.length - 1) {
        this.index++

      } else { 
        this.index = 0
        this.numCorrect = 0
        this.numTotal = 0
        this.getQuestionsFromAPI()
      }
      
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      } 
      this.numTotal++
    },
    getQuestionsFromAPI() {
        fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
          method: 'get'
        })
          .then((response) => {
            return response.json();
          })
          .then((jsonData) => {
            let questions = [...jsonData.results]
            console.log(questions)
            let shuffledQuestions = _.shuffle(questions)
            console.log(shuffledQuestions)
            this.questions = shuffledQuestions
            this.totalQuestions = jsonData.results.length
          })
    }
  },
  mounted: function() {
    this.getQuestionsFromAPI()
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
