<template>
  <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Введите число"/><br/>
  <button @click="convert()">КОНВЕРТИРОВАТЬ</button>
  <button @click="favourite()" className="fav-button">В ИЗБРАННОЕ</button>
</template>

<script>
export default {
  props: {
    changeAmount: {
      type: Function,
      required: true
    },
    convert: {
      type: Function,
      required: true
    },
    favourite: {
      type: Function,
      required: true
    },
  },
};
</script>

<style scoped></style>
