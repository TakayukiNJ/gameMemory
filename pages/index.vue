<template>
  <div class="container">
  <Card v-for="card in cardlist"
        :key="card.id" 
        :cardId="card.id"
        :num="card.num"
        :opa="card.opa"
        :face="card.face"
        :src="card.src"
        @click="clickCount"
  />
  </div>
</template>

<script>
import Card from "~/components/Card";

export default {
  components: {
    Card,
  },
  data() {
    return {
      cardlist: [{ 
        id: 1,
        num: 1,
        opa: 1,
        face: true,
        src: require("~/assets/cardFront.png"),
      }],
      cCount:0,
      cardlist1:[],
    };
    //表だったら、裏だったら、マークの柄の判定、数字の情報を入れる
  },
  mounted() {
    const Newcardlist = [];
    //カードを作る連想配列
    let count = 1;
    for (let i = 0; i < 52; i++) {
      count++;
      // https://qiita.com/artistan/items/9eb9a0fb14f4ec3a8764
      for (let i = Newcardlist.length-1; i >= 0; i--){
        let rand = Math.floor(Math.random() * (i + 1));
        // 配列の数値を入れ替える
        [Newcardlist[i], Newcardlist[rand]] = [Newcardlist[rand], Newcardlist[i]]
      }
      if (i % 13 == 0) count = 1;//13までいったらカウントを１に戻す。
      let a = { id: i + 1, num: count, opa:1, face:true, src:require("~/assets/cardFront.png") };
      Newcardlist.push(a);
    }
    this.cardlist = Newcardlist;
  },
  methods:{
    clickCount(num, cardId, opa, face, src){
      // 同じカードを引いた時
      if(this.cardlist1[2] == cardId){
        return;
      }
      if(face == false){
        return;
      }
      this.cCount++;
      // 最初のカードと2枚目のカードで条件分岐
      if(this.cCount % 2 !== 0){
        const NewcardlistFirst = this.cardlist.concat();
        const targetIndex = NewcardlistFirst.findIndex(cardlist => cardlist.id === cardId);
        this.cardlist1.push(num);         // 1枚目が何番のカードか保存
        this.cardlist1.push(targetIndex); // 1枚目が何番目にあるか保存
        this.cardlist1.push(cardId);      // 同じカードを引いた時用
        this.cardlist1.push(face);        // 1枚目が面にあるか保存
        this.cardlist1.push(src);         // 1枚目が面にあるか保存
        const Newcardlist = this.cardlist.concat();
        Newcardlist[targetIndex].src = require('~/assets/0/'+cardId+'.png');
        Newcardlist[targetIndex].face = false;
      } else {
        let cardlist2 = num;
        const targetIndex = this.cardlist1[1];
        const NewcardlistSecond = this.cardlist.concat();
        const targetIndex2 = NewcardlistSecond.findIndex(cardlist => cardlist.id === cardId);
        const Newcardlist = this.cardlist.concat();
        Newcardlist[targetIndex2].src = require('~/assets/0/'+cardId+'.png');
        Newcardlist[targetIndex2].face = false;
        // カードが揃った時と揃わなかった時で条件分岐
        if(cardlist2 == this.cardlist1[0]){
          this.cCount = 0;
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              alert("正解！\n1枚目のカード" + this.cardlist1[0] + "\n2枚目のカード" + cardlist2);
              Newcardlist[targetIndex].src = require("~/assets/cardFront.png");
              Newcardlist[targetIndex2].src = require("~/assets/cardFront.png");
              Newcardlist[targetIndex].opa = 0;  // 最初のカードを透明に
              Newcardlist[targetIndex2].opa = 0; // 2枚目のカードを透明に
              console.log(Newcardlist[targetIndex].src);
              this.cardlist1.length=null; // データを空にする
            }, 100)
          })
        }else{
          const Newcardlist = this.cardlist.concat();
          Newcardlist[targetIndex].face = true;  // 最初のカードを透明に
          Newcardlist[targetIndex2].face = true; // 2枚目のカードを透明に
          this.cCount = 0;
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              alert("残念！\n1枚目のカード" + this.cardlist1[0] + "\n2枚目のカード" + cardlist2);
              Newcardlist[targetIndex].src = require("~/assets/cardFront.png");
              Newcardlist[targetIndex2].src = require("~/assets/cardFront.png");
              this.cardlist1.length=null; // データを空にする
            }, 100)
          })
        }
      }
    }
  },
};
</script>

<style scoped>
.container {
  user-select: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgb(27, 145, 57);
  /* padding: 10px; */
  padding-left: 30px;
  padding-top: 5px;
}
</style>
