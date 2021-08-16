<template>
  <div id="app">
    <div name="0" v-on:click="greet" class="game__cell">{{ squares[0] }}</div>
      <div name="1" v-on:click="greet" class="game__cell">{{ squares[1] }}</div>
      <div name="2" v-on:click="greet" class="game__cell">{{ squares[2] }}</div>
      <div name="3" v-on:click="greet" class="game__cell">{{ squares[3] }}</div>
      <div name="4" v-on:click="greet" class="game__cell">{{ squares[4] }}</div>
      <div name="5" v-on:click="greet" class="game__cell">{{ squares[5] }}</div>
      <div name="6" v-on:click="greet" class="game__cell">{{ squares[6] }}</div>
      <div name="7" v-on:click="greet" class="game__cell">{{ squares[7] }}</div>
      <div name="8" v-on:click="greet" class="game__cell">{{ squares[8] }}</div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      counter: 0,
      squares: new Array(9).fill(1),
      count: Math.floor(Math.random() * (2)),
    }
  },
  methods: {
    greet(event) {
      let numberOfCell = event.target.getAttribute('name')
      this.squares[numberOfCell] = (this.count % 2 === 0) ? 'X' : 'O';
      this.count= this.count + 1;
      console.log(this.squares)
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
</style>
