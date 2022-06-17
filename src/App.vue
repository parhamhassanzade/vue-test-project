<template>
  <div id="app">
    <Header v-bind:index="this.index" />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <Content v-bind:CQ="questionList[index]" v-bind:next="next"
        /></b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from "./components/Header-main.vue";
import Content from "./components/Content-main.vue";

export default {
  name: "App",
  components: {
    Header,
    Content,
  },
  data() {
    return {
      questionList: [],
      index: 0,
    };
  },
  methods: {
    next() {
      if (this.index < 9) {
        this.index++;
      }
    },
  },
  mounted: function () {
    fetch("https://opentdb.com/api.php?amount=10&type=multiple", {
      method: "get",
    })
      .then((res) => {
        return res.json();
      })
      .then((result) => {
        this.questionList = result.results;
      });
  },
};
</script>


