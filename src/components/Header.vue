<template>
<div>
  <b-nav tabs>
    <b-nav-item active><b>VQuiz</b></b-nav-item>
    <b-nav-item>Score: {{numCorrect}}/{{numTotal}} </b-nav-item>
    <b-nav-item v-if="numCorrect > 0">Intelligence: {{perc}} % </b-nav-item>

  </b-nav>
</div>
</template>

<script>
export default {
  props:[
    'numCorrect',
    'numTotal',
    'correct_perc'
  ],
  computed:{
    perc: function () {
      return ((parseInt(this.numCorrect) / parseInt(this.numTotal)) * 100).toFixed(2)
    }
  }
}
</script>

<style>

</style>