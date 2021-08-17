<template>
  <div id="app">
      <select v-model="selected" v-if="isGameStarted === false">
        <option value="" >choose your color</option>
        <option value='red'>red</option>
        <option value='yellow'>yellow</option>
      </select>
      <button @click="startGame" v-if="isGameStarted === false">start game</button>
      <div class="game__square">
        <div
          v-on:click="() => greet(item)"
          class="game__cell"
          v-for="item in this.arr"
          :key="item.i"
          v-bind:style="style(item)"
        >{{ item.name }}</div>
        
      </div>
      <h1 v-if="this.isWon && !this.isDrow">player {{winner}} won!</h1>
      <h1 v-if="this.isDrow"> DROW </h1>
      <button @click="reloadPage">reload game</button>
       
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      isGameStarted: false,
      selected: '',
      count: 1,
      arr:   [{name:null,i:0},{name:null,i:1},{name:null,i:2},{name:null,i:3},{name:null,i:4},{name:null,i:5},{name:null,i:6},{name:null,i:7},{name:null,i:8}],
      pleyer: Boolean(this.count),
      isWon: false,
      winner: '',
      isDrow: false
    }
  },
  methods: {
    style(item) {
      if (!item.name) {
        return '';
      }
      console.log(this.selected)
      if (this.count % 2 === 0) 
      // ходимо перші
      {
        if(this.selected === 'red') {
          return (item.name === 'X' ? { background: 'red' } : { background: 'yellow' })
        }
        if(this.selected === 'yellow') {
          return (item.name === 'X' ? { background: 'yellow' } : { background: 'red' })
        }
      }
       if (this.count % 2 !== 0) // ходимо другі
       {
        if(this.selected === 'red') {
            return (item.name === 'O' ? { background: 'red' } : { background: 'yellow' })
          }
        if(this.selected === 'yellow') {
            return (item.name === 'O' ? { background: 'yellow' } : { background: 'red' })
          }
      }
    },
    startGame() {
      this.isGameStarted = true;
      if(this.count === 1) {
        this.arr[Math.floor(Math.random() *8)].name = 'X'
      } /// WTF?
    },
    greet(item) {
      if (item.name || this.isWon) {
        return
      }
      // if(!this.selected) {
      //   alert('YOU NEED TO CHOOSE A COLOR')
      //   return;
      // }
      // if(!this.isGameStarted) {
      //   alert('YOU NEED TO PRESS A BUTTON "START GAME"')
      //   return;
      // }
      // if(!this.isGameStarted && !this.selected) {
      //   alert('YOU NEED TO PRESS A BUTTON "START GAME" AND YOU NEED TO CHOOSE A COLOR')
      //   return;
      // }
        console.log(this.count)
        item.name = (this.count % 2 === 0) ? 'X' : 'O';
        this.count++
        let r = this.arr.filter(w => !w.name)[Math.floor(Math.random() * this.arr.filter(h=>!h.name).length)] 
        this.arr[r.i].name = (this.count % 2 === 0) ? 'X' : 'O';
        this.count++
        if(this.selected)
        this.winCheck()

      // if(this.count % 2 !== 0) {
      //   console.log(this.player)
      //   console.log(this.count)
      //   let r = this.arr.filter(w => !w.name)[Math.floor(Math.random() * this.arr.filter(h=>!h.name).length)] 
      //   this.arr[r.i].name = (this.count % 2 === 0) ? 'X' : 'O';
      //   this.count++
      //   item.name = (this.count % 2 === 0) ? 'X' : 'O';
      //   this.count++
      //   if(this.selected)
      //   this.winner()
      // }

    },
    winCheck() {
      // if (this.arr[0].name && this.arr[1].name && this.arr[2].name || this.arr[3].name && this.arr[4].name && this.arr[5].name) {
      //     this.isWon = true
      //     // window.location.reload();
      //     // alert('player win')
      // }

      // if (this.arr.slice(0, 3).every(win => win.name === 'X') || this.arr.slice(3, 6).every(win => win.name === 'X') || this.arr.slice(6, 9).every(win => win.name === 'X') 
      // || this.arr[0].name === 'X' && this.arr[3].name === 'X' && this.arr[6].name === 'X' || this.arr[1].name === 'X' && this.arr[4].name === 'X' && this.arr[7].name === 'X' || this.arr[2].name === 'X' && this.arr[5].name === 'X' && this.arr[8].name === 'X' 
      // || this.arr[0].name === 'X' && this.arr[4].name === 'X' && this.arr[8].name === 'X' || this.arr[2].name === 'X' && this.arr[4].name === 'X' && this.arr[6].name === 'X') {
      //   this.isWon = true;
      //   this.winner = 'X';
      // }
      // if (this.arr.slice(0, 3).every(win => win.name === 'O') || this.arr.slice(3, 6).every(win => win.name === 'O') || this.arr.slice(6, 9).every(win => win.name === 'O') 
      // || this.arr[0].name === 'O' && this.arr[3].name === 'O' && this.arr[6].name === 'O' || this.arr[1].name === 'O' && this.arr[4].name === 'O' && this.arr[7].name === 'O' || this.arr[2].name === 'O' && this.arr[5].name === 'O' && this.arr[8].name === 'O' 
      // || this.arr[0].name === 'O' && this.arr[4].name === 'O' && this.arr[8].name === 'O' || this.arr[2].name === 'O' && this.arr[4].name === 'O' && this.arr[6].name === 'O') {
      //   this.isWon = true;
      //   this.winner = 'O';
      // }
    
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
      const [a, b, c] = winningСombination[i];
      if (this.arr[a].name && this.arr[a].name === this.arr[b].name && this.arr[a].name === this.arr[c].name) {
        this.winner = this.arr[a].name;
        this.isWon = true;
      } else if (this.arr.every(player => player.name)){
        this.isDrow = true
      }
    }
    },
    reloadPage() {
      window.location.reload();
    },
    firstMove () {
      if(this.count % 2 !== 0) {
        let r = this.arr.filter(w => !w.name)[Math.floor(Math.random() * this.arr.filter(h=>!h.name).length)] 
        this.arr[r.i].name = (this.count % 2 === 0) ? 'O' : 'X';
        this.count++
      }
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.game__square {
  height: 300px;
  width: 300px;
  border: 1px solid black;
  margin: 50px auto;
  font-size: 110px;
  text-align: center;
  line-height: 100px;
  font-family: 'Indie Flower', sans-serif;
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
