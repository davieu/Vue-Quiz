<template>
  <div class="gameOver-div">
    <b-jumbotron>
      <!-- <template slot="lead">

      </template> -->

     <h1>You got {{ numCorrect }} out of {{ totalQuestions }} correct!</h1>
           <b-button 
        @click="next" 
        variant="success"
      >
        Restart
      </b-button>
      {{hello}}
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    next: Function,
    totalQuestions: String,
    numCorrect: String,
    hello: String
  }
}
</script>

<style scoped>
  .gameOver-div {
    margin-top: 100px;
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