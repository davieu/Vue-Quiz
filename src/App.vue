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
    <TriviaConfig 
      :categories="categories"
      :difficulty="difficulty"/>
        </b-col>
      </b-row>
    </b-container>

    <b-container class="bv-example-row" v-if="index < 10">
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
        <b-container class="bv-example-row" v-if="index >= 10">
      <b-row>
        <b-col xs="10" sm="10" offset-sm="1">
          <GameOver 
            :next="next"
            :numCorrect="numCorrect"
            :totalQuestions="totalQuestions"
            :hello="hello"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import GameOver from './components/GameOver.vue'
import TriviaConfig from './components/TriviaConfig.vue'
import _ from 'lodash'

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox,
    GameOver,
    TriviaConfig
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      totalQuestions: 0,
      categories: [
        'Any Category',
        'General Knowledge',
        'Entertainment: Books',
        'Entertainment: Film',
        'Entertainment: Music',
        'Entertainment: Musicals & Theatres',
        'Entertainment: Television',
        'Entertainment: Video Games',
        'Entertainment: Board Games',
        'Science & Nature',
        'Science: Computers',
        'Science: Mathematics',
        'Mythology',
        'Sports',
        'Geography',
        'History',
        'Politics',
        'Art',
        'Celebrities',
        'Animals',
        'Vehicles',
        'Entertainment: Comics',
        'Science: Gadgets',
        'Entertainment: Japanese Anime & Manga',
        'Entertainment: Cartoon & Animation'
      ],
      difficulty: [
        'Any',
        'Easy',
        'Medium',
        'Hard'
      ],
      amount: 10
    }
  },
  methods: {
    next() {
      if (this.index !== this.questions.length) {
        this.index++

      } else { 
        this.index++
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
            let shuffledQuestions = _.shuffle(questions)
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
  margin-top: 35px;
}
</style>
