<template>
    <v-container class="my-todo-list" fluid>
      <v-row justify="center">
        <v-col cols="12" md="8">
          <h1 class="title">Список моих Задач</h1>
          <v-form @submit.prevent="addTodo">
            <v-text-field v-model="newTodoTitle" label="Название Задачи" required></v-text-field>
            <v-textarea v-model="newTodoDescription" label="Описание Задачи"></v-textarea>
            <v-btn type="submit" color="primary">Добавить Задачу</v-btn>
          </v-form>
          <v-list dense>
            <v-list-item v-for="(todo, index) in todos" :key="index" class="todo-item">
              <v-list-item-content>
                <v-list-item-title :class="{ 'completed': todo.completed }">{{ todo.title }}</v-list-item-title>
                <v-list-item-subtitle v-if="todo.description">{{ todo.description }}</v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-action>
                <v-checkbox v-model="todo.completed"></v-checkbox>
                <v-btn icon @click="removeTodo(index)">
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    data() {
      return {
        todos: [],
        newTodoTitle: '',
        newTodoDescription: ''
      };
    },
    methods: {
      addTodo() {
        if (this.newTodoTitle.trim()) {
          this.todos.push({
            title: this.newTodoTitle,
            description: this.newTodoDescription,
            completed: false
          });
          this.newTodoTitle = '';
          this.newTodoDescription = '';
        }
      },
      removeTodo(index) {
        this.todos.splice(index, 1);
      }
    }
  };
  </script>
  
  <style scoped>
  .my-todo-list {
    background-color: #2c2c2e;
    color: #fff;
    min-height: 100vh;
    padding: 20px;
  }
  .title {
    text-align: center;
    margin-bottom: 20px;
  }
  .todo-item {
    background-color: #3a3a3c;
    border: 1px solid #444;
    margin-bottom: 10px;
    border-radius: 5px;
  }
  .completed {
    text-decoration: line-through;
    color: #777;
  }
  </style>
  