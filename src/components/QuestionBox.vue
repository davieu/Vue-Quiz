<template>
  <div class="questionBox-div">
    <b-jumbotron>
      <template slot="lead">
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">
      <b-list-group>
        <b-list-group-item 
          v-for="(answer, index) in answers" 
          :key="index"
          @click="selectAnswer(index)" 
          :class="answerClass(index)"
          :disabled="answered === true"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>
      
      <b-button 
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
      >
        Submit
      </b-button>
      <b-button 
        :disabled="!answered"
        @click="next" 
        variant="success"
      >
        Next
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
  import _ from 'lodash'
  export default {
    name: 'QuestionBox',
    props: {
      currentQuestion: Object,
      next: Function,
      increment: Function
    },
    data() {
      return {
        selectedIndex: null,
        correctIndex: null,
        shuffledAnswers: [],
        answered: false
      }
    },
    mounted() {
      console.log(this.currentQuestion)
    },
    computed: {
      answers() {
        //merging the incorrect and correct answer
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
        return this.shuffledAnswers
      }
    },
    watch: {
      currentQuestion: {
        immediate: true,
        handler() {
          this.selectedIndex = null
          this.answered = false
          this.shuffleAnswers()
          this.disableAnswers = false
        }
      }
    },
    methods: {
      selectAnswer(index) {
        this.selectedIndex = index
      },
      submitAnswer() {
        let isCorrect = false

        if (this.selectedIndex === this.correctIndex) {
          isCorrect = true
        }
        this.answered = true

        this.increment(isCorrect)
      },
      shuffleAnswers() {
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
        this.shuffledAnswers = _.shuffle(answers)
        this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
      },
      answerClass(index) {
        let answerClass = ''
        if (!this.answered && this.selectedIndex === index) {
          answerClass = 'selected'
        } else if (this.answered && this.correctIndex === index) {
          answerClass = 'correct'
        } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
          answerClass = 'incorrect'
        }

        return answerClass

        // IN TERNARY
        // !answered && selectedIndex === index ? 'selected' : 
        // answered && correctIndex === index ? 'correct' : 
        // answered && selectedIndex === index && correctIndex !== index ? 'incorrect' : ''
      }
    }
  }
</script>

<style scoped>
  .questionBox-div {
    margin-top:40px;
  }

  .list-group {
    margin-bottom: 15px; 
  }

  .list-group-item:hover {
    background: #EEE;
    cursor: pointer;
  }

  .btn {
    margin: 0 5px;
  }

  .selected {
    background-color: lightblue;
  }

  .correct {
    background-color: lightgreen;
  }

  .incorrect {
    background-color: red;
  }
</style>


