<template>
  <div>
    <header>
      <h1>Vue + TypeScript TODO</h1>
    </header>
    <main>
      <TodoInput
        :todoItem="todoTitle"
        @input="updateTodoTitle"
        @add="addTodo"
      ></TodoInput>
      <div>
        <ul>
          <TodoList
            v-for="(todoItem, index) in todoItems"
            :key="index"
            :todoItem="todoItem"
          ></TodoList>
        </ul>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import TodoInput from '@/components/TodoInput.vue';
import TodoList from '@/components/TodoList.vue';

const KEY = 'todo_key';

const storage = {
  save(toDo: Todo[]) {
    const parse = JSON.stringify(toDo);
    localStorage.setItem(KEY, parse);
  },
  fetch(): Todo[] {
    return JSON.parse(localStorage.getItem(KEY) || '[]');
  },
};

export interface Todo {
  title: string;
  done: boolean;
}

export default Vue.extend({
  components: { TodoList, TodoInput },
  data() {
    return {
      todoTitle: '',
      todoItems: [] as Todo[],
    };
  },
  created() {
    this.fetchTodoList();
  },
  methods: {
    updateTodoTitle(value: string) {
      this.todoTitle = value;
    },
    addTodo() {
      const todo: Todo = {
        title: this.todoTitle,
        done: false,
      };

      this.todoItems.push(todo);
      storage.save(this.todoItems);
      this.initForm();
    },
    initForm() {
      this.todoTitle = '';
      console.log(this.todoTitle);
    },
    fetchTodoList() {
      this.todoItems = storage.fetch();
    },
  },
});
</script>

<style scoped></style>
