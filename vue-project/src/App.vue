<template>
  <div>
    <h1>TIC TAC TOE</h1>
    <div class="game">
      <span class="game__section" v-for="(item, index) in board" @click="move(index)">
        {{ item }}
      </span>
    </div>
    <h3>{{ message || 'Turn ' + turn }}</h3>
    <button @click="restart">Restart</button>
</div>
</template>

<script>
export default {
  data() {
    return {
      board: [
        '', '', '',
        '', '', '',
        '', '', ''
      ],
      turn: 'X',
      message: null,
      game_over_bool: false
    }
  },
  methods: {
    move(index) {
      if (this.game_over_bool || this.board[index] != '') return

      this.board[index] = this.turn
      this.game_over_bool = this.game_over()
      this.turn = (this.turn === 'X') ? 'O' : 'X'
    },
    game_over() {
      const success_cases = [
        [0, 1, 2], [0, 3, 6], [0, 4, 8], [1, 4, 7],
        [2, 5, 8], [2, 4, 6], [4, 5, 6], [6, 7, 8]
      ]
      for (let s_case of success_cases) {
        const [a, b, c] = s_case
        if (this.board[a] == '') return false
        if (this.board[a] == this.board[b] && this.board[a] == this.board[c]) {
          this.message = 'The winner is player <' + this.turn + '>'
          return true
        }
      }
      for (let item of this.board) {
        if (item === '') {
          return false
        }
      }
      this.message = 'Draw'
      return true
    },
    restart() {
      this.board = [
        '', '', '',
        '', '', '',
        '', '', ''
      ]
      this.turn = 'X'
      message = null
      game_over_bool = false
    }
  }
}
</script>

<style>
.game {
  display: grid;
  grid-template-columns: repeat(3, 3fr);
  width: 300px;
}

.game__section {
  width: 100px;
  height: 100px;
  background-color: black;
  border: 1px #fff solid;
  opacity: .85;
  cursor: pointer;
  color: rgb(0, 255, 242);
  font-size: 64px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.game__section>div {
  width: 100%;
  height: 100%;
}

.game__section:hover {
  opacity: 1;
}

h1 {
  text-align: center;
  color: rgb(51, 51, 255);
}

h3 {
  text-align: center;
  font-size: 24px;
  color: rgb(17, 207, 17);
}
</style>
