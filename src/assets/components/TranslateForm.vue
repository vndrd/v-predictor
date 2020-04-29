<template>
  <div id="translateForm">
      <form v-on:submit="submitForm">
          <input type="text" v-model="textToTranslate" placeholder="Input you content here..." />
          <select v-model="language">
              <option value="en">English</option>
              <option value="ru">Russian</option>
              <option value="ko">Koran</option>
              <option value="ja">Japenese</option>
          </select>
          <input type="submit" value="Translate" />
      </form>
  </div>
</template>

<script>
export default {
  name: 'TranslateForm',
  data: function(){
      return {
          textToTranslate:"",
          language:'en'
      }
  },
  methods:{
      submitForm:function(e){
        //   alert(this.textToTranslate);
        this.$emit("formSubmit", this.textToTranslate, this.language);
        e.preventDefault();
      }
  }
}
</script>

<style>
</style>
