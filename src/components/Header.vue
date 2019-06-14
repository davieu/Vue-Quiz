<template>
  <div>
    <b-nav tabs >
      <b-nav-item disabled class="nav-header"><b>Quiz Your Mind</b></b-nav-item>
      <b-nav-item disabled>Correct: {{ numCorrect }}/{{ numTotal }}</b-nav-item>
      <b-nav-item disabled>Total Questions: {{ totalQuestions }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
  export default {
    name: 'Header',
    props: [
      'numCorrect',
      'numTotal',
      'totalQuestions'
    ]
  }
</script>
 
<style>
  .nav-header {
    margin-left: 30px
  }
</style>
