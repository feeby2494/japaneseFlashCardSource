<template>
  <b-container class="home">
    <b-row>
      <b-col>

        <HelloWorld msg="Check out changes to JLPT N5 Vocab! I added around 20 words and made a quiz app! Give it a test!"/>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
