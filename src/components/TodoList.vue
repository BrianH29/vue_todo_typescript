<template>
  <li>
    <span>{{ todoItem.title }}</span>
    <button @click="deleteTodo">DELETE</button>
  </li>
</template>

<script lang="ts">
import Vue, { PropType } from 'vue';
import { Todo } from '@/App.vue';

export default Vue.extend({
  props: {
    todoItem: {
      type: Object as PropType<Todo>,
    },
    index: {
      type: Number,
    },
  },
  methods: {
    deleteTodo() {
      this.$emit('deleteTodo', this.index);
    },
  },
});
</script>

<style scoped></style>
