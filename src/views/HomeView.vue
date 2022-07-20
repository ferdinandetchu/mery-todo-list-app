<template>
  <v-container style="height: 100vh">
    <v-row justify="center" align="center" class="fill-height">
      <v-card min-width="350" max-width="475" class="mx-auto">
        <!-- <h1>Todo List</h1> -->
        <v-toolbar color="teal" dark>
          <v-app-bar-nav-icon></v-app-bar-nav-icon>

          <v-toolbar-title>Todo List</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn v-if="!isAdd" fab small @click="isAdd = true">
            <v-icon> mdi-plus </v-icon>
          </v-btn>
        </v-toolbar>

        <v-text-field
          label="Input Todo"
          placeholder="What needs to be done?"
          solo
          append-icon="mdi-plus"
          ref="title"
          v-model="newTodo"
          v-if="isAdd"
          :rules="[() => !!newTodo || 'This field is required']"
          @click:append="addTodo()"
        ></v-text-field>

        <v-list subheader>
          <v-subheader class="red--text">Things Todo</v-subheader>
          <CheckList
            @check="ChangeState($event)"
            v-if="thingsTodo.length > 0"
            :todos="thingsTodo"
          />
        </v-list>

        <v-divider></v-divider>

        <v-list subheader>
          <v-subheader class="amber--text">Doing</v-subheader>
          <CheckList
            @check="ChangeState($event)"
            v-if="doingTodo.length > 0"
            :todos="doingTodo"
          />
        </v-list>

        <v-divider></v-divider>
        <v-list subheader>
          <v-subheader class="green--text">Done</v-subheader>
          <CheckList
            @check="ChangeState($event)"
            v-if="doneTodo.length > 0"
            :todos="doneTodo"
          />
        </v-list>
      </v-card>
    </v-row>
  </v-container>
</template>

<script>
// import { filter } from "vue/types/umd";
import CheckList from "../components/CheckList";

export default {
  name: "HomeView",

  components: {
    CheckList,
  },
  data: () => ({
    isAdd: false,
    newTodo: "",
    todo: [
      {
        todoState: "todo",
        title: "Create Website",
      },
      {
        todoState: "doing",
        title: "Create Build",
      },
      {
        todoState: "done",
        title: "Create confirm",
      },
    ],
  }),
  computed: {
    doingTodo() {
      return this.todo.filter((x) => x.todoState == "doing");
    },
    doneTodo() {
      return this.todo.filter((x) => x.todoState == "done");
    },
    thingsTodo() {
      return this.todo.filter((x) => x.todoState == "todo");
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.length > 0) {
        // console.log("you");
        this.todo.unshift({ todoState: "todo", title: this.newTodo });
        this.newTodo = "";
      } else {
        // this.$refs.title.validate();
        console.log("me");
      }
    },
    ChangeState(state) {
      console.log(state.todoState);
    },
  },
};
</script>
