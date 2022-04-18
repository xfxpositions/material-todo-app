<template>
  <v-app>
    <v-container>
      <v-card class="mx-auto" max-width="800" tile>
        <v-card-title>Todo App</v-card-title>
        <template v-for="(todo, index) in todos" :key="todo">
          <v-list-item v-if="!todo.complete">
            <v-list-item-header>
              <v-list-item-title>{{ todo.name }}</v-list-item-title>
            </v-list-item-header>
            <v-list-item-content>
              <v-btn @click="completeTodo(index)" class="ma-2" dark>
                <v-icon dark right> mdi-checkbox-marked-circle </v-icon>
              </v-btn>
            </v-list-item-content>
          </v-list-item>
        </template>

        <v-text-field
          ref="user_text"
          v-model="user_text"
          label="Type a new todo"
        ></v-text-field>
        <v-btn @click="newTodo()">Add New Todo</v-btn>
        <v-btn @click="showCompleteTodos = !showCompleteTodos"
          >{{ showCompleteTodos ? "Show" : "Hide" }} Complete Todos</v-btn
        >
      </v-card>
      <v-card v-if="showCompleteTodos" class="mx-auto" max-width="800">
        <v-card-title>Completed todos</v-card-title>
        <template v-for="(todo, index) in todos" :key="todo">
          <v-list v-if="todo.complete">
            <v-list-item>
              <v-list-item-title>{{ todo.name }}</v-list-item-title>
            </v-list-item>
            <v-list-item-content>
              <v-btn @click="completeTodo(index)" class="ma-2" dark>
                Uncomplete
              </v-btn>
            </v-list-item-content>
          </v-list>
        </template>
      </v-card>
    </v-container>
  </v-app>
</template>
<script>
export default {
  data() {
    return {
      showCompleteTodos: false,
      user_text: null,
      todos: [
        {
          name: "example",
          complete: false,
        },
      ],
    };
  },
  methods: {
    newTodo() {
      if (this.user_text) {
        this.todos.push({
          name: this.user_text,
          complete: false,
        });
        this.user_text = "";
      }
    },
    completeTodo(todoIndex) {
      this.todos[todoIndex].complete = !this.todos[todoIndex].complete;
    },
  },
};
</script>
