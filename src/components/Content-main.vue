<template>
  <div>
    <b-jumbotron>
      <template>Question:{{ CQ.question }}</template>

      <hr class="my-4" />
      <b-list-group>
        <b-list-group-item
          v-for="(answer, i) in shuffledAnswers"
          :key="i"
          @click="chengeIndex(i)"
          v-bind:class="[Cindex === i ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#" @click="submitAnswer">submit</b-button>
      <b-button @click="next" variant="success" href="#">next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  props: {
    CQ: Object,
    next: Function,
  },
  data() {
    return {
      Cindex: null,
      shuffledAnswers: [],
      correctAnswer: [],
    };
  },
  methods: {
    chengeIndex(i) {
      this.Cindex = i;
    },
    shuffleAnswers() {
      let answers = [...this.CQ.incorrect_answers, this.CQ.correct_answer];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctAnswer = this.shuffledAnswers.indexOf(this.CQ.correct_answer);
    },
    submitAnswer() {
      if (this.Cindex === this.correctAnswer) {
        alert("true");
      }else{
        alert("false")
      }
    },
  },
  computed: {
    answers() {
      let answers = [...this.CQ.incorrect_answers];
      answers.push(this.CQ.correct_answer);
      return answers;
    },
  },
  // watch: {
  //   CQ() {
  //     this.Cindex = null;
  //   },
  // },
  watch: {
    CQ: {
      immediate: true,
      handler() {
        this.Cindex = null;
        this.shuffleAnswers();
      },
    },
  },
};
</script>

<style scoped>
.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}
.btn {
  margin: 10px 5px;
}
.selected {
  background: lightblue;
}
</style>
