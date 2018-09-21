<template>
  <img :src="src" class="card" @click="clickCarda()" :style="`opacity: ${opa}`"/>
</template>

<script>
export default {
  data(){
    return{
      src:require("~/assets/cardFront.png"),
    }
  },
  props:['cardId','num','opa','face','src'],
    methods:{
      clickCarda(){
        this.src = require('~/assets/0/'+this.cardId+'.png');
        this.$emit('click',this.num,this.cardId, this.opa, this.face, this.src);
        console.log();
        // this.opa = 0.5;
      },
    },
}
</script>

<style >
.card {
  /* デフォルトの値を宣言*/
  /* --card-image: url("../../assets/nakajoMemory/cardFront.png");
  background-image: var(--card-image); */
  width: 100px;
  height: auto;
  padding: 3.5px;
  /* background: url('~/assets/cardFront.png'); */
}
</style>
