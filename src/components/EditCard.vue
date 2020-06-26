<template>
  <div id="editCard">
    <h2>Edit this card!</h2>
    <form v-if="initialValues">
      <div class="form-group">
        <label>Vocab in Kanji: </label>
        <input type="text" :value="initialValues.word" @input='updateWord'></input>
        <p> Inputed value: {{ newValues.word }}</p>
        <label>Vocab in only hiragana: </label>
        <input type="text" :value="initialValues.hiragana" @input='updateHiragana'></input>
        <p> Inputed value: {{ newValues.hiragana }}</p>
        <br>
        <label>Sentence with Kanji using vocab word: </label>
        <input type="text" :value="initialValues.sentence" @input='updateSentence'></input>
        <p> Inputed value: {{ newValues.sentence }}</p>
        <label>Furigana for sentence: </label>
        <input type="text" :value="initialValues.furigana" @input='updateFurigana'></input>
        <p> Inputed value: {{ newValues.furigana }}</p>
        <br>
        <label>English word: </label>
        <input type="text" :value="initialValues.englishWord" @input='updateEnglishWord'></input>
        <p> Inputed value: {{ newValues.englishWord }}
        <label>Sentence in English: </label>
        <input type="text" :value="initialValues.englishSentence" @input='updateEnglishSentence'></input>
        <p> Inputed value: {{ newValues.englishSentence }} </p>
        <div class="button-group">
          <button type="button" @click.prevent="clearForm">
            クリア
          </button>
          <button type="submit" v-model="newValues" @click.prevent="onSubmit">送信</button>
        </div>
        <p>CardId: {{ $route.params.cardId }}</p>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'EditCard',
  props: {
    word: String,
    hiragana: String,
    sentence: String,
    furigana: String,
    englishWord: String,
    englishSentence: String,
    link: String,
  },
  data() {
    return {
      initialValues: {
        word: this.word,
        hiragana: this.hiragana,
        sentence: this.sentence,
        furigana: this.furigana,
        englishWord: this.englishWord,
        englishSentence: this.englishSentence
      },
      newValues: {
        word: '',
        hiragana: '',
        sentence: '',
        furigana: '',
        englishWord: '',
        englishSentence: '',
      },
      apiParam: this.$route.params.cardId
    };
  },
  methods: {
    updatePost(object) {
      for( const item in object ) {
        if( object.hasOwnProperty(item)) {
          if(object[item] === null || object[item] === '') {
            delete object[item];
          }
        }
      }
    },
    submitNewCardData() {
      this.updatePost(this.newValues);
      //need to update card in json
    },
    updateWord(event) {
      this.initialValues.word = event.target.value;
      this.newValues.word = this.initialValues.word;
    },
    updateHiragana(event) {
      this.initialValues.hiragana = event.target.value;
      this.newValues.hiragana = this.initialValues.hiragana;
    },
    updateSentence(event) {
      this.initialValues.sentence = event.target.value;
      this.newValues.sentence = this.initialValues.sentence;
    },
    updateFurigana(event) {
      this.initialValues.furigana = event.target.value;
      this.newValues.furigana = this.initialValues.furigana;
    },
    updateEnglishWord(event) {
      this.initialValues.englishWord = event.target.value;
      this.newValues.englishWord = this.initialValues.englishWord;
    },
    updateEnglishSentence(event) {
      this.initialValues.englishSentence = event.target.value;
      this.newValues.englishSentence = this.initialValues.englishSentence;
    },

    onSubmit() {
      this.submitNewCardData();
    },
    clearForm(event) {
      console.log("I'm clearing the form");
      console.log(this.newValues.word);
      this.submitted = false;
      this.initialValues.word= this.word;
      this.newValues.word= this.word;
      this.initialValues.hiragana= this.hiragana;
      this.newValues.hiragana= this.hiragana;
      this.initialValues.sentence= this.sentence;
      this.newValues.sentence= this.sentence;
      this.initialValues.furigana= this.furigana;
      this.newValues.furigana= this.furigana;
      this.initialValues.englishWord= this.englishWord;
      this.newValues.englishWord= this.englishWord;
      this.initialValues.englishSentence= this.englishSentence;
      this.newValues.englishSentence= this.englishSentence;
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
    width: 100%;
    padding: 1.5rem;
    border: solid 1px grey;
    margin: 2px 0;
  }
  #editCard {
    margin: 1rem;
    border: solid 1px grey;
    display: flex;
    flex-direction: column;
  }
  .form-group {
    margin: 1rem;
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
  }
  .form-group p {
    align-self: flex-start;
  }

  @media (min-width: 700px) {
    .button-group {
      margin-top: auto;
      margin-bottom: 0;
      display: flex;
      flex-direction: row;
      flex: 1 30%;
      max-height: 80px;

    }
  }

</style>
