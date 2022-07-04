<template>
  <div>
    <h1>Tic-Tac-Toe (Vite + Composables)</h1>
    <header v-if='calculateWinner' class='header'>
      <h2>
        {{ calculateWinner }}
      </h2>
    </header>
    <h2 v-else>Next Up: {{ playerValue }}</h2>
    <button class="reset" @click="reset">Play again</button>
    <div class='board'>
      <span class='vertical-line-1'></span>
      <span class='vertical-line-2'></span>
      <Square
        v-for='(square, i) in board'
        :key='`square-${i}`'
        :label="`square-${i}`"
        :value='square'
        @click='markSquare(i)'
        :winner="calculateWinner"
      />
      <span class="confetti"></span>
    </div>
  </div>
</template>

<script>
  import Square from './Square.vue'
  import { defineComponent } from 'vue'
  import { useBoard } from '../composables/useBoard'
  import { useCalculateWinner } from '../composables/useCalculateWinner'

  export default defineComponent({
    components: {
      Square,
    },
  
    setup() {
      // separate logic out with composables
      const { board, playerValue, markSquare, reset } = useBoard()
      const { calculateWinner } = useCalculateWinner(board)

      return {
        board,
        playerValue,
        markSquare,
        calculateWinner,
        reset,
      }
    }
  })
</script>

<style scoped>
  .header {
    display: grid;
    gap: 1rem;
  }
  .reset {
    background: #35495e;
    border: none;
    border-radius: 5px;
    padding: 1rem 1.5rem;
    color: white;
    text-transform: uppercase;
  }
  .board {
    position: relative;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    max-width: 480px;
    margin: 50px auto;
  }

  span.confetti {
    position:relative;
    left:250px;
    top:-160px;
  }

  .board::before, .board::after {
    background: linear-gradient(to right,  #41b883, #35495e)
  }

  .vertical-line-1, .vertical-line-2 {
    background: linear-gradient(to right,  #41b883, #35495e)
  }

  .board::before, .board::after {
    content: '';
    width: 100%;
    height: 5px;
    position: absolute;
    border-radius: 1rem;
  }

  .board::before {
    top: 33%;
  }

  .board::after {
    top: 66%;
  }

  .vertical-line-1, .vertical-line-2 {
    position: absolute;
    width: 100%;
    height: 5px;
    top: 50%;
    border-radius: 1rem;
    transform: translate(-50%, -50%) rotate(90deg);
  }

  .vertical-line-1 {
    left: 33%;
  }

  .vertical-line-2 {
    left: 66%;
  }
</style>