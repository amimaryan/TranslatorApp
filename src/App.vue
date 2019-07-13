<template>
  <div id="app">
    <h1> Word Translator </h1>
    <h5> Powered by Vue.js</h5>
    <TranslateForm v-on:formSubmit="TranslateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'App',
  components:{
    TranslateForm,
    TranslateOutput
  },
  data: function(){
    return {
      translatedText:''
    }
  },
  methods: {
    TranslateText:function(text){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20190713T213342Z.5252712e2b191a40.abd2008f8455d70eb027b956f49e43cca11ff77d&lang=ru&text=' + text)
      .then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
#app {
}
</style>
