<template>  
  <div id="app">
    <h1>Translate Online</h1>
    <h5 class="text-muted">Fast / Accurate / Easy</h5>
    <TranslateForm v-on:formSubmit="textTranslate"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'
export default {
  name: 'App',
  data:function(){
    return {
      translatedText:''
    }
  },
  components:{
    TranslateForm,
    TranslateOutput
  },
  methods:{
    textTranslate: function(text, language){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20191023T041315Z.38a463b02eff9e3d.662f966205410571b5e42f58d43c13d6f138ef22&lang='+language+'&text='+text).then((res)=>{
        this.translatedText = res.body['text'][0];
      });
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
