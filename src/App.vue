<template v-if="this.question">
  <div>
    <ScoreBoard :winCount="this.winCount" :loseCount="this.loseCount" />
    <h1 v-html="this.question"></h1>
    <div v-for="(answer, index) in this.answers" v-bind:key="index">
      <input :disabled="this.answerSubmitted" type="radio" name="options" :value="answer" v-model="this.chosenAnswer">
      <label v-html="answer"></label><br>
    </div>
    <button v-if="!this.answerSubmitted" @click="this.submitAnswer()" class="send" type="button">Send</button>
    <AnswerComponent />
  </div>
  
</template>

<script>
  import ScoreBoard from '@/components/ScoreBoard.vue'
  import AnswerComponent from '@/components/AnswerComponent.vue'
  
  export default {
    name: 'App',

    components: {
      ScoreBoard,
      AnswerComponent
    },

    data() {
      return {
        question: undefined,
        incorrectAnswers: undefined,
        correctAnswer: undefined,
        chosenAnswer: undefined,
        answerSubmitted: false,
        winCount: 0,
        loseCount: 0
      }
    },

    computed: {
      answers() {
        var answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
        answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswer);
        return answers;
      }
    },

    methods: {
      submitAnswer() {
        if(!this.chosenAnswer) {
          alert('Select one of the options bellow!');
        } else {
          this.answerSubmitted = true;
          if(this.chosenAnswer == this.correctAnswer) {
            this.winCount++;
          } else {
            this.loseCount++;
          }
        }
      },
      getNewQuestion() {
        this.answerSubmitted = false; // redefinir a resposta enviada e tirar a section
        this.chosenAnswer = undefined;
        this.question = undefined;

        this.axios.get('https://opentdb.com/api.php?amount=20').then((response) => {
          this.question = response.data.results[0].question;
          this.incorrectAnswers = response.data.results[0].incorrect_answers;
          this.correctAnswer = response.data.results[0].correct_answer;
        })
      }
    },

    created() {
      this.getNewQuestion();
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
    color: black;
    margin: 60px auto;
    max-width: 600px;
  }

  input {
      margin: 10px;
  }

  button {
      margin-top: 10px;
      background-color: white; 
      color: black; 
      border: 2px solid #008CBA;
      border-radius: 4px;
      padding: 5px 24px;
  }

  button:hover {
      background-color: #008CBA;
      color: white;
      cursor: pointer;
  }

</style>
