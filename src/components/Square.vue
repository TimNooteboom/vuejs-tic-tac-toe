<template>
  <button
    class="square"
    :name="label"
    :disabled='winner || value'>
    {{ value }}
  </button>
</template>


<script>
export default {
  props: {
    label: String,
    value: {
      type: String,
      default: ' ',
    },
    winner: null,
  },
}
</script>


<style scoped>
  .square {
    border: none;
    width: 10rem;
    height: 10rem;
    background: none;
    color: inherit;
    font-size: 3rem;
    font-weight: 700;
  }

  .square:hover {
    cursor: pointer;
  }

  .square:focus {
    outline: none;
    background: #41b88330;
  }

  .square:first-child,
  .square:nth-child(2),
  .square:nth-child(3) {
    border-top: none;
  }

  .square:nth-child(3),
  .square:nth-child(6),
  .square:last-child {
    border-right: none;
  }

  .square:nth-child(7),
  .square:nth-child(8),
  .square:last-child {
    border-bottom: none;
  }

  .square:first-child,
  .square:nth-child(4),
  .square:nth-child(7) {
    border-left: none;
  }
</style>