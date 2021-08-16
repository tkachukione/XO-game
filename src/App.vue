<template>
  <div id="app">
      <select v-model="selected" v-if="isGameStarted === false">
        <option value="" >choose your color</option>
        <option value='true'>red</option>
        <option value='false'>blue</option>
      </select>
      <button @click="startGame" v-if="isGameStarted === false">start game</button>
      <div class="game__square" v-if="!this.isWon">
        <div
          v-on:click="() => greet(item)"
          class="game__cell"
          v-for="item in this.arr"
          :key="item.i"
          v-bind:style="style(item)"
        >{{ item.name }}</div>
        
      </div>
      <h1 v-if="this.isWon">YOU WIN</h1>
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
      counter: 0,
      count: Math.floor(Math.random() * (2)),
      arr:   [{name:null,i:0},{name:null,i:1},{name:null,i:2},{name:null,i:3},{name:null,i:4},{name:null,i:5},{name:null,i:6},{name:null,i:7},{name:null,i:8}],
      pleyer: Boolean(this.count),
      isWon: false
      
    }
  },
  methods: {
    style(item) {
      if (!item.name) {
        return '';
      }
      // if (this.selected) {
      //   return this.count % 2 === 0 ? { background: 'red' } : { background: 'yellow' }
      // } 
      // if (!this.selected) {
      //   return this.count % 2 === 0 ? { background: 'yellow' } : { background: 'red' }
      // }
      // if (this.selected && item.name === 'O') {
      //   return { background: 'red' }
      // }
      // else {
      //   return { background: 'yellow' }
      // }
      // return  item.name === 'X' ? { background: 'red' } : { background: 'yellow' }
      console.log(this.selected)
      if (this.count % 2 === 0) {
        return ((item.name === 'X' && this.selected) ? { background: 'red' } : { background: 'yellow' })
      }
       if (this.count % 2 !== 0) {
        return ((item.name === 'O' && !this.selected) ? { background: 'red' } : { background: 'yellow' })
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
        this.winner()

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
    winner() {
      if (this.arr[0].name && this.arr[1].name && this.arr[2].name || this.arr[3].name && this.arr[4].name && this.arr[5].name) {
          this.isWon = true
          // window.location.reload();
          // alert('player win')
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
