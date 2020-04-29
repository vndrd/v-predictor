<template>  
  <div>
    <b-row class="justify-content-md-center">
      <b-col md="4" >
        <select v-model="language" class="form-control">
            <option value="es">Español</option>
            <option value="en">English</option>
        </select>
        <vue-bootstrap-typeahead 
        class="mt-4"
          v-model="query"
          :data="aaaa"
        />
      </b-col>
    </b-row>
  </div>
</template>
<script>
import VueBootstrapTypeahead from 'vue-bootstrap-typeahead'
export default {
  name: 'TranslateForm',
  props:['aaa'],
  data: function(){
      return {
          textToComplete:"",
          language:'es',
          query:'',
          example: ['Canad', 'USA', 'Mexico','Caminon','Cata']
      }
  },
  mounted: function(){
    console.log('qwe')
  },
  methods:{
      completeText:function(event){
        console.log('name:',event.key)
        if(event.key == "ArrowDown") {
          this.$emit("completeText", this.textToComplete, this.language);
        }
      }
  },
  components: {
    VueBootstrapTypeahead
  },
  computed: {
    aaaa: function() {
      return this.aaa
    },
  },
  watch: {
    query: function(val) {
      if(val) {
        console.log('we goin', val)
        this.$emit("completeText", this.query, this.language);
      }
    },
    
  }
}
</script>

<style lang="scss" scoped>
input[type='text']{
  padding: 1rem;
  border-radius: .5rem;
}
input[type='submit']{
  padding: 1rem;
  border-radius: .5rem;
  border: 0px;
}
.list-group-item {
    border: 1px solid rgba(0, 0, 0, 0);
}
</style>

