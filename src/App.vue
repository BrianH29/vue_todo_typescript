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
            :index="index"
            :todoItem="todoItem"
            @deleteTodo="deleteTodo"
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
import { Todo } from './interface';

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
    deleteTodo(index: number) {
      this.todoItems.splice(index, 1);
      storage.save(this.todoItems);
    },
  },
});
</script>

<style scoped></style>
