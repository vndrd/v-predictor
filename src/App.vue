<template>  
  <div id="app">
    <h1>Predictor online</h1>
    <TranslateForm v-on:completeText="textCompleted" :aaa="aaa"></TranslateForm>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import debounce from 'debounce' 
export default {
  name: 'App',
  data:function(){
    return {
      translatedText:'',
      temporal: '',
      aaa:  []
    }
  },
  created: function(){
    this.textCompleted = debounce(this.textCompleted,300)
  },
  components:{
    TranslateForm,
  },
  methods:{
    textCompleted: function(text, language){
      let textModi = text.replace(/_/g, text)
      this.$http.get(`https://predictor.yandex.net/api/v1/predict.json/complete?key=pdct.1.1.20200428T024500Z.0dcf5b55e588de70.37231757c2be5b43ca7678ff72582f0d88d06d38&q=${textModi}&lang=${language}`).then((res)=>{
        this.translatedText = res.body['text'][0]
        this.aaa.push(res.body['text'][0])
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
