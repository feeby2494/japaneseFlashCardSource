<template>
  <b-container>
      <b-row v-if="!cardObject" id="vocablist">
        <b-col sm="6" lg="4" class="mb-3" v-for="word in $options.japaneseVocab.n5_vocab" :key="word.id">
          <div class="card" style="width: 18rem;">
            <div class="card-header" v-if="word.kanji">{{ word.kanji }}</div>
            <div class="card-header" v-if="!word.kanji">{{ word.kana }}</div>
            <div class="card-body">
              <p v-if="word.kanji" class="card-text">{{ word.kana }}</p>
              <p class="card-text">{{ word.eng }}</p>
              <br v-if="!word.kanji">
            </div>
          </div>
        </b-col>
      </b-row>
      <b-row v-if="cardObject" class="my-5">

      </b-row>

      <b-row id="flashcards">
        <b-col id="quiz" v-if="quizStats.finished === false">
          <b-jumbotron header="Quiz" lead="JLPT N5 Vocab">
            <b-row>
              <b-col class="flashcard " v-if="cardObject">
                <h5>Score: {{ quizStats.score }}</h5>
                <h3>{{ cardObject.kanji}}</h3>
                <h3 v-if="!cardObject.kanji">{{ cardObject.kana }}</h3>
                <b-form-input type="text" name="kana" value="hiragana for this?" v-model="userInput"></b-form-input>
              </b-col>
            </b-row>
            <b-row class="mt-4">
              <b-col>
                <b-button v-if="cardObject" class="mr-3" squared variant="info" type="button" name="check" v-on:click="quiz($event, userInput, cardObject, quizStats, changeCard)">Check Answer</b-button>
                <b-button squared variant="success" v-if="!cardObject" type="button" name="button" v-on:click="changeCard($event)">Start Quiz</b-button>
              </b-col>
            </b-row>
          </b-jumbotron>
        </b-col>
        <b-col id="finishedQuiz" v-if="quizStats.finished === true">
          <b-jumbotron header="Quiz" lead="JLPT N5 Vocab">
            <h3>Congradualations! All correct!</h3>
            <b-button squared variant="info" type="button" name="startOver" v-on:click="startOver($event, quizStats)">Start Over</b-button>
          </b-jumbotron>
        </b-col>
      </b-row>
      <b-row class="mt-3">

      </b-row>
  </b-container>

</template>

<script>
// @ is an alias to /src
// import FlashCardInput from '@/components/FlashCardInput.vue'
// import FlashCard from '@/components/FlashCard.vue'
import japaneseVocab from '@/json/japaneseVocab.json'

export default {
  name: 'Vocab',
  components: {
    // FlashCard,
    // FlashCardInput
  },
  japaneseVocab: japaneseVocab,
  data () {
    return {
      flashcards : null,
      title: "Japanese Vocab",
      showInput: false,
      dataChanged: false,
      manageMode: false,
      cardObject: null,
      userInput: null,
      quizStats: {
        score: 0,
        wrongAnswers: [],
        correctAnswers: [],
        quizCounter: 0,
        correctStatus: false,
        finished: false
      }
    };
  },

  methods: {
    changeCard: function(event, quizStats, ...args) {
      let selectedCard;

      function randomNumber(array) {
        return Math.floor(Math.random() * (array.length));
      }

      function didAlready(arrayOfRight, randomCard){
        let testArray = arrayOfRight.map((card) => {
          return ((card.id == randomCard.id) ? true : false);
        });
        return ((testArray.every(x => x === false)) ? false : true );
      }

      function selectNewCard(array){
        let idSelection = randomNumber(array);
        return japaneseVocab.n5_vocab[idSelection];
      }

      function clearInput() {
        return '';
      }

      function notEndOfQuiz(correctArray, cardsInQuiz){
        return ((correctArray.length < cardsInQuiz.length) ? true : false );
      }
      console.log(japaneseVocab.n5_vocab.length);
      selectedCard = selectNewCard(japaneseVocab.n5_vocab);



      if(args[0]) {
        if (notEndOfQuiz(args[0], japaneseVocab.n5_vocab) === false) {
          return quizStats.finished = true;
        }
        while( didAlready(args[0], selectedCard)) {
          console.log("switched card again")
          selectedCard = selectNewCard(japaneseVocab.n5_vocab);
        }
        this.userInput = clearInput();
        return this.cardObject = selectedCard;
      } else {
        this.userInput = clearInput();
        return this.cardObject = selectedCard;
      }
    },
    quiz: function(event, userAnswer, card, quizStats, switchCard) {
      function checkAnswer(userInput, correctAnswer, quizStats, nextCard){
        if(userInput === correctAnswer){
          quizStats.score++;
          quizStats.quizCounter++;
          quizStats.correctStatus = true;
          quizStats.correctAnswers.push(card);
          nextCard(event, quizStats, quizStats.correctAnswers);
          return quizStats;
        } else {
          quizStats.quizCounter++;
          quizStats.wrongAnswers.push(card);
          nextCard(event, quizStats, quizStats.correctAnswers);
          quizStats.correctStatus = false;
          return quizStats;
        }
      }
      // if( quizStats.correctAnswers.length === japaneseVocab.n5_vocab.length) {
      //   return quizStats.finished = true;
      // }
      if(card.kanji) {
        return checkAnswer(userAnswer, card.kana, quizStats, switchCard);
      } else {
        return checkAnswer(userAnswer, card.eng, quizStats, switchCard);
      }
    },
    startOver: function(event, quizStats) {
      quizStats = {
        score: 0,
        wrongAnswers: [],
        correctAnswers: [],
        quizCounter: 0,
        correctStatus: false,
        finished: false
      };
      this.userInput = '';
      return this.quizStats = quizStats;
    },
  },
  mounted() {
    this.updateCards();
  },

}
</script>

<style scoped>

 </style>
