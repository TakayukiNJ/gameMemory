<template>
  <div class="main">
    <div class="board">
      <div>
        <div
         class="cell"
         v-for="i in Math.pow(grid, 2)"
         :key="i"
         :style="`width: ${100 / grid}%`"
        >
          <div @click="putPiece(i)">
            <div
              class="piece"
              v-if="getUserId(i)"
              :style="`background-color: ${colors[i]}`"
            >{{ getUserId(i) }}</div>
            <!-- <div class="piece" v-if="i % 2 === 1">{{ i }}</div> -->
            <!-- <div class="piece" v-if="getUserId(i)">{{ getUserId(i) }}</div> -->
            <!-- </div> -->
            <!-- :は式を返す -->
          </div>
          <div @click='send(i)'>
            <div class='piece' v-if='getUserId(i)'>{{ getUserId(i) }}</div>
          </div>
        </div>
      </div>
    </div>
    <ColorPalette
     :list="colorList"
     :current="currentColorIndex"
     @select="changeColorIndex"
    />
    <UserSelector
     :number='number'
     :current='currentUser'
     @change='changeCurrentUser'
    />
  </div>
</template>

<script>
// import ColorPalette from '~/components/nakajo/ColorPalette.vue';
// import UserSelector from '~/components/nakajo/UserSelector.vue';

export default {
  components: {
    // ColorPalette,
    // UserSelector,
  },
  async asyncData({ app }) {
    const mypath = process.env.NAKAJO_PATH;
    const board = await app.$axios.$get(`${mypath}/board`);
    // console.log(board);
    return {
      mypath,
      board,
      // grid: 19,
      number: 16,
      // currentUser: 1,
    };
  },
  data() {
    const grid = 25;
    const colors = [];
    for (let i = 0; i < grid ** 2; i += 1) {
      colors.push('#fff');
    }
    return {
      grid,
      colors,
      colorList: ['#0f0', '#f00', '#000', '#fff'],
      currentColorIndex: 0,
    };
  },
  // mounted() {
  //   setInterval(() => {
  //     this.grid = this.grid + 1;
  //   }, 1000);
  // },
  computed: {
    getUserId() {
      return (i) => {
        const xaxis = ((i - 1) % this.grid) - (Math.ceil(this.grid / 2)) + 1;
        const yaxis = ((Math.ceil(this.grid / 2)) - Math.floor((i - 1) / this.grid) + 1);
        // const n = i ** 2;
        // // idx === current ? '#0ff' : ''
        // // const n = mypath;
        // return n;
        for (let j = 0; j < this.board.length; j += 1) {
          const piece = this.board[j];
          if (piece.x === xaxis && piece.y === yaxis) {
            return piece.userid;
          }
        }
        return false;
      };
    },
  },
  methods: {
    changeColor(i) {
      const newColors = [...this.colors];
      newColors[i] = this.colorList[this.currentColorIndex];
      this.colors = newColors;
    },
    changeColorIndex(index) {
      console.log(this.changeColorIndex);
      this.changeColorIndex = index;
      console.log(this.changeColorIndex);
    },
    // changeColorIndex2(index) {
    //   this.changeColorIndex = index;
    // },
    async putPiece() {
      const x = 1;
      const y = 2;
      const userid = 5;

      // キドさんが考えたのに依存する
      const params = new URLSearchParams();
      params.append('x', x);
      params.append('y', y);
      // params.append('x', xaxis);
      // params.append('y', yaxis);
      params.append('userid', userid);

      this.board = await this.$axios.$post(`${this.mypath}/piece`, params, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
        },
      });
    },
    // キドさんの分
    async send(i) {
      const xaxis = ((i - 1) % this.grid) - (Math.ceil(this.grid / 2)) + 1;
      const yaxis = ((Math.ceil(this.grid / 2)) - Math.floor((i - 1) / this.grid) + 1);
      const params = new URLSearchParams();
      params.append('x', xaxis);
      params.append('y', yaxis);
      // params.append('userid', 100);
      params.append('userid', this.currentUser);

      this.board = await this.$axios.$post(`${this.mypath}/piece`, params, {
        headers: {
          'Content-Type': 'application/x-www-form-urlencoded',
        },
      });
    },
    changeCurrentUser(n) {
      this.currentUser = n;
    },
  },
};
</script>

<style>
.main {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: auto;
  background: rgb(27, 145, 57);
}

.board{
  padding-top: 100%;
  position: relative;
}

.board > div {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.cell {
  display: inline-block;
  border: 1px solid #333;
  vertical-align: bottom;
}

.cell > div {
  padding-top: 100%;
  position: relative;
}

.piece{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 50%;
  width: 60%;
  height: 60%;
  background: #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #444;
  font-size: 120%;
  font-weight: bold;
}
</style>
