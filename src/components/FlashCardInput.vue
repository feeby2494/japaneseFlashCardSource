<template>
  <div id="flashcardInput">
    <form >
      <div class="form-group">
        <label>Vocab in Kanji: </label>
        <input type="text" :value="postBody.word" @input='updateWord'></input>
        <p> Inputed value: {{ postBody.word }}</p>
        <label>Vocab in only hiragana: </label>
        <input type="text" :value="postBody.hiragana" @input='updateHiragana'></input>
        <p> Inputed value: {{ postBody.hiragana }}</p>
        <br>
        <label>Sentence with Kanji using vocab word: </label>
        <input :value="postBody.sentence" @input='updateSentence'></input>
        <p> Inputed value: {{ postBody.sentence }}</p>
        <label>Furigana for sentence: </label>
        <input :value="postBody.furigana" @input='updateFurigana'></input>
        <p> Inputed value: {{ postBody.furigana }}</p>
        <br>
        <label>English word: </label>
        <input :value="postBody.englishWord" @input='updateEnglishWord'></input>
        <p> Inputed value: {{ postBody.englishWord }}
        <label>Sentence in English: </label>
        <input :value="postBody.englishSentence" @input='updateEnglishSentence'></input>
        <p> Inputed value: {{ postBody.englishSentence }} </p>
        <div class="button-group">
          <button type="button" @click.prevent="clearForm">
            クリア
          </button>
          <button type="submit" v-model="postBody" @click.prevent="onSubmit">送信</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'FlashCardInput',
  props: {
    word: String,
    hiragana: String,
    sentence: String,
    furigana: String,
    englishWord: String,
    englishSentence: String,
  },
  data() {
    return {
      postBody: {
        word: '',
        hiragana: '',
        sentence: '',
        furigana: '',
        englishWord: '',
        englishSentence: ''
      }
    };
  },
  methods: {
    updateWord(event) {
      this.postBody.word = event.target.value;
    },
    updateHiragana(event) {
      this.postBody.hiragana = event.target.value;
    },
    updateSentence(event) {
      this.postBody.sentence = event.target.value;
    },
    updateFurigana(event) {
      this.postBody.furigana = event.target.value;
    },
    updateEnglishWord(event) {
      this.postBody.englishWord = event.target.value;
    },
    updateEnglishSentence(event) {
      this.postBody.englishSentence = event.target.value;
    },
    onSubmit() {
      //need to push need card to json
    },
    clearForm(event) {
      console.log("I'm clearing the form");
      console.log(this.postBody.word);
      this.submitted = false;
      this.postBody.word= '';
      this.postBody.hiragana= '';
      this.postBody.sentence= '';
      this.postBody.furigana= '';
      this.postBody.englishWord= '';
      this.postBody.englishSentence= '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #flashcardInput {
    margin: 1rem;
    border: solid 1px grey;
    display: flex;
    flex-direction: column;
  }
  button-group {
    width: 100;
  }
  button {
    width: 95%;
    padding: 1.5rem;
    border: solid 1px grey;
    margin: 2px 1px;
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

  }



</style>
