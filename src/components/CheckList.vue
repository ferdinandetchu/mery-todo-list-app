<template>
  <div>
    <v-list-item v-for="(todo, index) in todos" :key="index">
      <v-list-item-action>
        <v-checkbox
          @click="checkedTodo(todo)"
          input-value
          color="primary"
        ></v-checkbox>
      </v-list-item-action>
      <v-list-item-content>
        <v-list-item-title>{{ todo.title }}</v-list-item-title>
        <!-- <v-list-item-subtitle>Descrition</v-list-item-subtitle> -->
      </v-list-item-content>
      <v-list-item-icon>
        <v-btn icon>
          <v-icon> mdi-message-outline </v-icon>
        </v-btn>
      </v-list-item-icon>
    </v-list-item>
  </div>
</template>

<script>
export default {
  name: "CheckList",
  props: {
    todos: Array,
  },
  // data: () => ({}),
  // emits: ["check"],
  methods: {
    checkedTodo(todo) {
      this.$emit("check", todo);
      // console.log(todo);
    },
  },
};
</script>
