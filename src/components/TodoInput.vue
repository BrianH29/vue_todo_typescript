<template>
  <div>
    <label for="write-todo"></label>
    <input
      id="write-todo"
      type="text"
      :value="todoItem"
      @input="handleInput"
      @keyup.enter="add"
    />
    <button @click="add">submit</button>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  props: {
    todoItem: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleInput(event: any) {
      this.$emit('input', event.target.value);
    },
    add() {
      this.$emit('add');
    },
  },
});
</script>

<style scoped></style>
