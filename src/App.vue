<template>
  <div id="app" class="app">
      <select class="select" v-model="selected" v-if="!isGameStarted">
        <option value="" >choose your color</option>
        <option value='red'>red</option>
        <option value='yellow'>yellow</option>
      </select>
      <button class="button" @click="startGame" v-if="!isGameStarted">start game</button>
      <div class="game__square">
        <div
          v-on:click="() => onClick(item)"
          class="game__cell"
          v-for="item in this.board"
          :key="item.i"
          :style="style(item)"
        >{{ item.name }}</div>
      </div>
      <h1 v-if="this.winner && !this.isDrow">player {{winner}} won!</h1>
      <h1 v-if="this.isDrow && !this.winner"> DROW </h1>
      <button class="reload__button" @click="reloadPage">reload game</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    const rand =  Math.floor(Math.random() * (2));
    return {
      isGameStarted: false,
      selected: '',
      playerMove: rand,
      firstMoveChance: rand,
      board:   
      [
        {name:null,i:0},
        {name:null,i:1},
        {name:null,i:2},
        {name:null,i:3},
        {name:null,i:4},
        {name:null,i:5},
        {name:null,i:6},
        {name:null,i:7},
        {name:null,i:8}
      ],
      winner: '',
    }
  },
  methods: {
    style(item) {
      if (!item.name) {
        return '';
      }
      const otherColor = this.selected === 'red' ? 'yellow' : 'red';
      if (this.firstMoveChance % 2 === 0) 
      {
        return (item.name === 'X' ? { background: this.selected } : { background: otherColor })
      } else {
        return (item.name === 'O' ? { background: this.selected } : { background: otherColor })
      }
    },
    startGame() {
      if (!this.selected) {
         alert('YOU NEED TO CHOOSE A COLOR')
        return;
      }
      this.isGameStarted = true;
      if(this.firstMoveChance === 1) {
        this.board[Math.floor(Math.random() *8)].name = 'X'
      }
    },
    onClick(item) {
      if (item.name || this.winner) {
        return;
      }
      if(!this.selected) {
        alert('YOU NEED TO CHOOSE A COLOR')
        return;
      }
      if(!this.isGameStarted) {
        alert('YOU NEED TO PRESS A BUTTON "START GAME"')
        return;
      }
        item.name = (this.playerMove % 2 === 0) ? 'X' : 'O';
        this.playerMove++
        this.winCheck()
        if (!this.winner) {
          const randomSortedboarday = this.board.filter(item => !item.name)[Math.floor(Math.random() * this.board.filter(element=>!element.name).length)] 
          this.board[randomSortedboarday.i].name = (this.playerMove % 2 === 0) ? 'X' : 'O';
          this.playerMove++
          if(this.selected)
          this.winCheck()
        }
    },
    winCheck() {
      const winningСombination = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let i = 0; i < winningСombination.length; i++) {
        const [x, y, z] = winningСombination[i];

        const isWon = this.board[x].name === this.board[y].name && this.board[x].name === this.board[z].name;

        if (this.board[x].name && isWon) {
          this.winner = this.board[x].name;
          return;
        }
      }
      if (this.board.every(player => player.name)) {
        this.isDrow = true;
        return;
      }
    },
    reloadPage() {
      window.location.reload();
    },
  }
}

</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 160px;
}
.game__square {
  height: 300px;
  width: 300px;
  border: 1px solid black;
  margin: 100px auto 0;
  font-size: 110px;
  text-align: center;
  line-height: 100px;
  font-family: 'Indie Flower', sans-serif;
}
.select {
  display: block;
  left: calc(50% - 70px);
  margin-bottom: 20px;
  position: absolute;
  top: 50px;
  box-sizing: border-box;
  width: 140px;
}
.button {
  display: block;
  left: calc(50% - 70px);
  margin-bottom: 20px;
  position: absolute;
  top: 90px;
  box-sizing: border-box;
  width: 140px;
}
.reload__button {
  position: absolute;
  top: 550px;
  box-sizing: border-box;
  width: 140px;
  left: calc(50% - 70px);
}
.red{
  background: red;
}

.blue{
  background: blue;
}
.game__cell {
  height: 100px;
  width: 100px;
  border: 1px solid black;
  float: left;
  box-sizing: border-box;
}

</style>
