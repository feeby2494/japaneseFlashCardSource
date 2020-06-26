<template>
  <section id="flashcards-body">
    <h1>{{ title | capitalize }}</h1>
    <div id="flashcard">
      <FlashCard
        v-model="card"
        :key="card._id"
        :word="card.word"
        :hiragana="card.hiragana"
        :sentence="card.sentence"
        :furigana="card.furigana"
        :englishWord="card.englishWord"
        :englishSentence="card.englishSentence"/>
      <!-- <EditCard
        v-model="card"
        :key="card._id"
        :word="card.word"
        :hiragana="card.hiragana"
        :sentence="card.sentence"
        :furigana="card.furigana"
        :englishWord="card.englishWord"
        :englishSentence="card.englishSentence"
        :link="this.$route.params.cardId"/> -->
    </div>
  </section>

</template>

<script>
// @ is an alias to /src
import FlashCard from '@/components/FlashCard.vue';
import EditCard from '@/components/EditCard.vue';

export default {
  name: 'Vocab',
  components: {
    FlashCard,
    EditCard
  },
  data () {
    return {
      card : {},
      newCards : {},
      title: "Single Vocab Word",
      apiParam: this.$route.params.cardId
    };
  },
  mounted() {
    //need to get specific card from json
  },

}
</script>

<style scoped>

  #flashcards-body {
    max-width: 1000px;

  }
  #flashcard {
    width: 100%;
    justify-content: center;
    display: flex;
    flex-direction: column;

  }
  @media (min-width: 800px) {
    #flashcard {
      flex-direction: row;
      align-items: flex-start;
    }
  }


</style>
