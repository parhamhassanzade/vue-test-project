<template>
  <div>
    <b-jumbotron>
      <template>Question:{{ CQ.question }}</template>

      <hr class="my-4" />

      <p v-for="answer in answers" :key="answer">{{answer}}</p>

      <b-button variant="primary" href="#">submit</b-button>
      <b-button @click="next" variant="success" href="#">next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    CQ: Object,
    next: Function,
  },
  computed: {
    answers() {
      let answers = [...this.CQ.incorrect_answers];
      answers.push(this.CQ.correct_answer);
      return answers;
    },
  },
};
</script>
