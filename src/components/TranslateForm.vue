<template>
  <div id="translateForm"> 
     <form v-on:submit="formSubmit">
        <input type="text" v-model="textToTranslate" placeholder="Enter a Word">
<select v-model="language">
  <option v-for="(item, index) in languageList" :key="item.id" :value="index">
     {{item}}
  </option>
</select>
        <input type ="submit" value="Translate">
     </form>
  </div>
</template>

<script>

export default {
  name: 'translateForm',
  data(){
      return {
          textToTranslate:'',
          language:'',
          languageList:[]
      }
  },
  created(){
    this.language = 'ru';
  },
  mounted(){
    this.$http
    .get('https://translate.yandex.net/api/v1.5/tr.json/getLangs?key=trnsl.1.1.20190713T213342Z.5252712e2b191a40.abd2008f8455d70eb027b956f49e43cca11ff77d&ui=en')
        .then(response => {
          console.log(response.body.langs);
          this.languageList = response.body.langs;
        });   
  },
  methods: {
      formSubmit(e){
          this.$emit('formSubmit', this.textToTranslate, this.language);
          e.preventDefault();
      }
   },
}
</script>

<style>

</style>
