<template>
  <div>
    <b-jumbotron>
      <template slot="lead">
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">
      <b-list-group>
        <b-list-group-item v-for="(answer, index) in answers" :key="index">{{ answer }}</b-list-group-item>
      </b-list-group>
      <!-- <p v-for="(answer, index) in answers" :key="index">
        {{ answer }}
      </p> -->

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
  export default {
    name: 'QuestionBox',
    props: {
      currentQuestion: Object,
      next: Function
    },
    computed: {
      answers() {
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)

        let currentIndex = answers.length, temporaryValue, randomIndex;

        // While there remain elements to shuffle...
        while (0 !== currentIndex) {

        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = answers[currentIndex];
        answers[currentIndex] = answers[randomIndex];
        answers[randomIndex] = temporaryValue;
        }
        return answers
      }
    },
    mounted() {
      console.log("mounted", this.currentQuestion)
    }
  }
</script>

<style scoped>
  .list-group {
    margin-bottom: 15px; 
  }
  .btn {
    margin: 0 5px;
  }
</style>


