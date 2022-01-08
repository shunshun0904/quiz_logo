<template>
  <div id="app">
    <div class="offset-3 col-6">
      <div class="card">
        <div class="card-body">
          <p class="badge badge-dark">第 {{ questionIndex + 1 }} 問</p>
          <br />
          <h4 class="card-title">
            <img :src="currentQuestion.logoUrl" />
          </h4>
          <hr />
          <button
            type="button"
            class="btn btn-primary btn-lg btn-block text-left"
            v-for="(answer, index) in currentQuestion.answers"
            v-bind:key="index"
            @click="addAnswer(index)"
          >
            {{ index + 1 }}. {{ answer }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "App",
  data: function () {
    return {
      answers: [],
      questionIndex: 0,
      questions: [
        {
          logoUrl: require("@/assets/img/roma.png"),
          answers: ["白い石", "黒い石", "どちらも同じ"],
          answer: 1,
        },
        {
          logoUrl: require("@/assets/img/arsenal.png"),
          answers: ["N", "L", "V"],
          answer: 0,
        },
        {
          logoUrl: require("@/assets/img/bayern.png"),
          answers: ["OK", "オーケストラ", "おけら"],
          answer: 1,
        },
      ],
    };
  },
  methods: {
    addAnswer: function (index) {
      this.answers.push(index);

      if (this.questions.length == this.answers.length) {
        var correctCount = 0;

        for (var i in this.answers) {
          var answer = this.answers[i];

          if (answer == this.questions[i].answer) {
            correctCount++;
          }
        }

        alert(correctCount + "問正解です！");
      } else {
        this.questionIndex++;
      }
    },
  },
  computed: {
    currentQuestion: function () {
      return this.questions[this.questionIndex];
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>