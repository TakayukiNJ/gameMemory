<template>
  <div class="main">
    <div id="app_sample">
      <p v-bind:class="pClass">v-bind:class</p>
      <p v-bind:style="pStyle">v-bind:style</p>
      <!-- <p>氏名：<input type="text" required></p>
      <p>フリガナ：<input type="text" required></p>
      <p>性別：
        男<input type="radio" value="男" name="seibetu">
        女<input type="radio" value="女" name="seibetu">
      </p>
      <p>生年月日：
        西暦<input type="text" name="year">年
        <input type="text" name="month">月
        <input type="text" name="date">日
        <input type="text" name="age">歳
        </p>
      <p>住所：
        〒<input type="text" name="address1" required>-
        <input type="text" name="address2" required><br>
        住所<input type="text" name="address3" required>
      </p>
      <p>Email：<input type="text" name="mail" required></p>
      <p>ご希望のプレゼント：<input type="select" required></p> -->
    </div>
    <div id="app">
        <div class="row_1st">
            <div
            v-for="card in allCards"
            :key="card.id"
            :id="card.id"
            @click="flip(card)"/>
        </div>
        <!-- v-vind:style="styleObject"
            v-bind:style="{ 'background-image': 'url(./assets/nakajoMemory/cardFront.png)' }"
             -->
    </div>
    <button @click="gameStart">start</button>
    
  </div>
</template>

<script>

// import Logo from '~/components/memory/Memory.vue';
import backgroundUrl from '~/assets/nakajoMemory/0/1.png';

export default {
//   var app = new Vue({
//   el: "#app",
 
//   data: {
//     pClass: "red",
//     pStyle: {
//       "font-weight": "bold",
//       "color": "#0f0"
//     }
//   }
// })
  components: {
    // Logo,
    backgroundUrl,
  },
  data() {
    return {
      allCards: [],
      styleObject: {
        backgroundImage: 'https://www.google.co.jp/search?q=tranp&num=30&source=lnms&tbm=isch&sa=X&ved=0ahUKEwiz7bCvj7rdAhVBObwKHXdeBj0Q_AUICigB&biw=671&bih=680#imgrc=Z2ovWMHk5MVsEM:',
      },
    };
  },
  computed: {
    styles() {
      return {
        // '--card-image': 'url("../../assets/nakajoMemory/0/1.png")',
        // '--width': this.width,
      };
    },
  },
  methods: {
    gameStart() {
      for (let heart = 0; heart < 13; heart += 1) {
        this.allCards.push({
          id: heart,
          number: heart + 1,
          pattern: 0,
          face: false,
        });
      }
      for (let diamond = 0; diamond < 13; diamond += 1) {
        this.allCards.push({
          id: diamond + 13,
          number: diamond + 1,
          pattern: 1,
          face: false,
        });
      }
      for (let clova = 0; clova < 13; clova += 1) {
        this.allCards.push({
          id: clova + 26,
          number: clova + 1,
          pattern: 2,
          face: false,
        });
      }
      for (let spade = 0; spade < 13; spade += 1) {
        this.allCards.push({
          id: spade + 39,
          number: spade + 1,
          pattern: 3,
          face: false,
        });
      }
      console.log(this.allCards);
    },
    flip(card) {
      for (let i = 0; i < 52; i += 1) {
        if (card.id === 0 && this.allCards[i].id === 0) {
        // ここにCSSを変えるプログラミングを入れたい。
        //   data: {
        //     styleObject: {
        //       width: '50px';
        //       height: '70px';
        //     };
        //   }
        //   this.styleObject.backgroundImage = url("../../assets/nakajoMemory/0/1.png");
          // backgroundImage: 'url("../../assets/nakajoMemory/0/1.png")', // "" で括っていないとIEでは表示されない
        //   console.log(this.allCards[i].id);
        //   console.log(card.id);
          console.log('ok');
        }
      }
    },
  },
};
</script>

<style>
#app {
  margin: 10px;
}
.main {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: auto;
  background: rgb(27, 145, 57);
}
ul {
  list-style: none;
}
#app > .row_1st > #1 {
  background-image: url("../../assets/nakajoMemory/0/1.png");
}
.row_1st > div {
  /* デフォルトの値を宣言*/
  --card-image: url("../../assets/nakajoMemory/cardFront.png");
  background-image: var(--card-image);
  width: 50px;
  height: 70px;
  background-size:cover;
  background-position:center;
  display:inline-block;
  vertical-align: middle;
}

</style>
