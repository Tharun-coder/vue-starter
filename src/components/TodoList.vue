<template>
  <div class="container">
    <div class="row">
      <div class="col-12"><p class="display-3">Todo List App</p></div>
    </div>
    <div class="row">
      <CreateTodo @on-addTodo="addTodo($event)" />
    </div>
    <div class="row">
      <div class="col-12 col-lg-6">
        <ul class="list-group">
          <TodoItem
            v-for="(todo, index) in todos"
            :key="index"
            :todoString="todo.todoString"
            :completed="todo.completed"
            @on-delete="deleteTodo(todo)"
            @on-toggle="toggleTodo(todo)"
            @on-edit="editTodo(todo, $event)"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import CreateTodo from "./CreateTodo.vue";
export default {
  components: {
    TodoItem,
    CreateTodo,
  },
  data() {
    return {
      todos: [
        { todoString: "Learn Vue", completed: false },
        { todoString: "Connect to VPN & DB", completed: true },
        { todoString: "Do local setup of repos", completed: false },
      ],
    };
  },
  methods: {
    addTodo(newTodo) {
      this.todos.push({
        todoString: newTodo,
        completed: false,
      });
    },
    toggleTodo(todo) {
      todo.completed = !todo.completed;
    },
    editTodo(todo, newTodoString) {
      todo.todoString = newTodoString;
    },
    deleteTodo(deleteTodo) {
      this.todos = this.todos.filter(
        (e) => e.todoString !== deleteTodo.todoString
      );
    },
  },
};
</script>

<style></style>
