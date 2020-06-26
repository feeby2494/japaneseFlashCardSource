<template>
  <div id="flashcards">
    <div class="cardText">
      <div v-if="!showEnglish" class="Japanese">
        <h2 v-if="showFurigana">{{ hiragana }}</h2>
        <h2 v-else>{{ word }}</h2>
        <br>
        <h2 v-if="showFurigana">{{ furigana }}</h2>
        <h2 v-else>{{ sentence }}</h2>
        <br>
      </div>
      <br>
      <h2 v-if="showEnglish">{{ englishWord }}</h2>
      <h2 v-if="showEnglish">{{ englishSentence }}</h2>
      <br>
    </div>
    <div class="button-group">
      <button v-on:click="showFurigana = !showFurigana">Show / hide Furigana</button>
      <button v-on:click="showEnglish = !showEnglish">Show / hide English</button>
      <button v-if="link" @click="showCard(link)">Show card</button>
      <button v-if="!link" @click="showAll">Back to Vocab List</button>
      <button v-if="manageMode" @click="deleteCard(link)">Delete Card</button>
    </div>
  </div>
</template>

<script>



export default {
  name: 'FlashCard',
  data () {
    return {
      showFurigana: false,
      showEnglish: false
    };
  },
  props: {
    id: String,
    word: String,
    hiragana: String,
    sentence: String,
    furigana: String,
    englishWord: String,
    englishSentence: String,
    link: String,
    manageMode: false
  },
  methods: {
    showCard(link) {
      this.$router.push('/vocab/' + link);
      console.log(link);
    },
    showAll() {
      this.$router.push('/vocab');
    },
    deleteCard(link) {
      //delete card from json
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  button-group {
    width: 100;
  }
  button {
    width: 95%;
    padding: 1.5rem;
    border: solid 1px grey;
    margin: 2px 1px;
  }
  #flashcards {
    margin: 1rem;
    border: solid 1px grey;
    display: flex;
    flex-direction: column;

  }
  .cardText {

  }

  @media (min-width: 700px) {
    .button-group {
      margin-top: auto ;
      margin-bottom: 1rem;
      margin-left: 1rem;
      margin-right: 1rem;
      display: flex;
      flex-direction: row;
      flex: 1 30%;
      max-height: 80px;
      align-self: flex-end;
    }

    button {

    }
  }

</style>
