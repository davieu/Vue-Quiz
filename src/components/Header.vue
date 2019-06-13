<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><b>Quiz Your Mind</b></b-nav-item>
      <b-nav-item disabled>Counter {{ numCorrect }}/{{ numTotal }}</b-nav-item>
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

</style>
