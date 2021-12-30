<template>
  <li>
    <span>{{ todoItem.title }}</span>
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
  },
});
</script>

<style scoped></style>
