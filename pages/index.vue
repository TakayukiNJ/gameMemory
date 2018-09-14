<template>
  <div
    class="container"
  >
  <!-- v-for=”[i. 任意の名前] in [ii. data内の配列の名前]” -->
  <Card v-for="card in cardlist"
        :key="card.id" 
        :cardId="card.id"
        :left="card.left"
        :top="card.top"
        :num="card.num"
        @click="clickCount"
  />
  </div>
</template>

<script>
import Card from "~/components/Card";
// import Omocard from "~/components/OmoCard";
export default {
  components: {
    Card,
  },
  data() {
    return {
      // cardlist: [{ id: 1, left: 4, top: 2 }, { id: 2, left: 4, top: 2 }]
      cardlist: [{ 
        id: 1,
        left: 4,
        top: 2,
        num: 1,
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
        // 0~iのランダムな数値を取得
        let rand = Math.floor(Math.random() * (i + 1));
        // 配列の数値を入れ替える
        [Newcardlist[i], Newcardlist[rand]] = [Newcardlist[rand], Newcardlist[i]]
      }
      if (i % 13 == 0) count = 1;//13までいったらカウントを１に戻す。
      // let count = Math.floor(Math.random() * 13)
      let a = { id: i + 1, left: 3, top: 2, num: count };
      Newcardlist.push(a);//
      //  console.log(a);
    }
    this.cardlist = Newcardlist;//
  },
  methods:{
    clickCount(num1,cardId){
      // console.log(cardId);
       this.cCount++;
      //  console.log(this.cCount);
      
       if(this.cCount % 2 ==0){
          let cardlist2 =num1;
        //  let cardList2= num1;
          console.log("1だよ"+this.cardlist1[0]);
          console.log("2だよ"+cardlist2);
          if(cardlist2 == this.cardlist1[0]){
           alert("正解！");//この２つを消す
           const Newcardlist = this.cardlist.concat();
          //  console.log(Newcardlist);
           const targetIndex = Newcardlist.findIndex(cardlist=>cardlist.id===cardId);
           console.log(targetIndex);
           Newcardlist.splice(this.targetIndex,1);
           this.cardlist = Newcardlist;

          //  this.cardlist1.length=null;
          //  this.cardlist2.length=null;
         }else{
           //この２つを裏に戻す
           this.cardlist1.length=null;
          //  cardList2,this.cardList1[0],require("~/assets/cardFront.png");
         }
        //  alert(this.cCount+"ぐうすう");
        //  alert(this.num);
         //偶数だったら判定して、truuだったら消える、truuじゃなかったら裏に戻す。
       }
       else{
         this.cardlist1.push(num1);
        //  alert(this.cCount+"きすう");
       }
    }
    
  },
  

};
// console.log(list);
</script>

<style scoped>
.container {
  user-select: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: center/cover url("~/assets/haikei.jpg");
}
</style>
