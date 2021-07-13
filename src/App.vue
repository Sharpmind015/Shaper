<template>
  <div class="container">
    <Sidebar @toggle-sidebar="handleToggle" :toggle="toggle">
      <div>
        <h1 class="app-header">Shaper</h1>
        <form @submit.prevent="createShape">
          <label class="label" for="shapes">
            Choose shape
            <select class="input" required v-model="selected" value="selected" name="shapes" id="">
              <option disabled value="">Choose shape</option>
              <option :key="shape" v-for="shape in shapes" :value="shape">{{shape}}</option>
            </select>
          </label>
          <label class="label" for="stroke">
            Choose color {{selected}}
            <input required v-model="color" name="stroke" class="color" type="color">
          </label>
          <label class="label" v-if="selected === 'Square'" for="square">
            Length
            <input class="input" required v-model="squareLength" name="square" type="number" placeholder="Type length">
          </label>
          <label class="label" v-else-if="selected === 'Circle'" for="circle">
            Radius
            <input class="input" required v-model="radius" type="number" name="circle" placeholder="Type radius">
          </label>
          <label class="label" v-else-if="selected === 'Rectangle'" for="rectangle">
            Dimensions
            <input class="input" required v-model="rectangleWidth" type="number" name="rectangle" placeholder="Type width">
            <input class="input" required v-model="rectangleHeight" type="number" name="rectangle" placeholder="Type height">
          </label>
          <button class="btn" type="submit">Draw shape</button>
          <button @click="clearBoard" class="btn" type="button">Clear board</button>
        </form>
      </div>
    </Sidebar>
    <div class="board">
      <Board :key="index" :shape="shape" v-for="(shape, index) in board"></Board>
      <button @click="handleToggle" class="draw-btn">Draw</button>
    </div>
  </div>
</template>

<script>
import Board from './components/Board';
import Sidebar from './layouts/Sidebar';
export default {
  name: 'App',
  data() {
    return {
      board: [],
      selected: 'Square',
      shapes: ['Rectangle', 'Square', 'Circle'],
      color: '#0f5ff7',
      radius: 100,
      squareLength: 250,
      rectangleWidth: 200,
      rectangleHeight: 100,
      toggle: false
    }
  },
  components: {
    Board,
    Sidebar
  },
  methods: {
    createShape() {
      const { selected, color, radius, squareLength, rectangleHeight, rectangleWidth } = this;
      this.board = [...this.board, { selected, color, radius, squareLength, rectangleHeight, rectangleWidth }];
      this.handleToggle();
    },
    handleToggle() {
      this.toggle = !this.toggle;
    },
    clearBoard() {
      this.board = [];
      this.handleToggle();
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700;900&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-thumb {
  background: #0f5ff7;
}

html {
  font-size: 62.5%;
}

body {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

input,
select {
  width: 100%;
  background-color: #e2e6f8;
  font-size: 1.6rem;
  padding: 0px 11px;
  border-width: initial;
  border-style: none;
  border-color: initial;
  border-image: initial;
  outline: none;
  border-radius: 4px;
}

button {
  color: #ffffff;
  font-size: 1.7rem;
  outline: none;
  border: none;
}

.container {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-wrap: wrap;
  overflow: hidden;
}

.app-header {
  font-size: 3rem;
  font-weight: 700;
  color: #efedf0;
  margin: 2rem 0;
  text-transform: uppercase;
}

.board {
  position: relative;
  width: 60%;
  height: 100%;
  overflow-y: scroll;
  display: flex;
  flex-wrap: wrap;
  padding: 3rem;
  background-color: #ffffff;
  border: 5px solid #0f5ff7;
}

.draw-btn {
  display: block;
  position: fixed;
  bottom: 30px;
  right: 20px;
  color: #0f5ff7;
  border: 2px solid #0f5ff7;
  padding: 0.75rem 1rem;
}

.label {
  font-size: 1.8rem;
  display: block;
  margin-bottom: 2rem;
}

.input,
.color {
  margin-top: 1.5rem;
}

.input {
  padding: 1rem;
  height: 5rem;
}

.color {
  padding: 0;
  width: 5rem;
  height: 5rem;
  display: block;
}

.btn {
  display: block;
  margin-bottom: 1rem;
  width: 100%;
  background-color: #0f5ff7;
  padding: 15px 20px;
}

@media screen and (max-width: 1000px) {
  .board {
    width: 100%;
    padding-block-end: 1.3rem;
    border-width: 3px;
  }
}

@media screen and (min-width: 1000px) {
  .draw-btn {
    display: none;
  }
}
</style>
