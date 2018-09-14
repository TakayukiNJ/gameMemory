<template>
<!-- <div >{{name}} -->

<!-- <img :id="`cardId${cardId}`" src="~/assets/cardFront.png" class="card" style="left:100px" @click="clickCard()" /> -->

<img :src="src" class="card" @click="clickCarda()"/>
<!-- <img src="~/assets/0/[0].png" class="card"/> -->
    
</template>

<script>
export default {
  data(){   
    return{
      src:require("~/assets/cardFront.png"),
    }
  },
  props:['left','top','cardId','num'],
    methods:{
      clickCarda(eventa){
        // alert("a"+this.num);
        this.src = require('~/assets/0/'+this.cardId+'.png');
        // this.list.push(this.num)
        this.$emit('click',this.num,this.cardId);//thisでおくる方法ぐぐる
        // alert(countZ);
        // console.log(this.cardId);
      },
      // clickCardb(eventb){
      //   alert("b"+this.num);
      //   // let countZ = this.num;
      //   this.src = require('~/assets/0/'+this.cardId+'.png');
      //   this.$emit('click',this.num);//thisでおくる方法ぐぐる
      //   // alert(countZ);
      // },
      
    },
}
</script>

<style >
.card {
  /* position: absolute; */
  width: 100px;
  height: auto;
  /* background: url('~/assets/cardFront.png'); */
}

</style>
