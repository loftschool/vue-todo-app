<template lang="pug">
  div
    div.todo
      todo-input
      todo-list(
        v-if="todos.length > 0"
        :todos="filteredTodos"
      )
</template>
<script>
import todoInput from "./todoInput";
import todoList from "./todoList";
import { mapState, mapGetters, mapActions } from "vuex";
export default {
  data() {
    return {
      // todos: [],
      // filter: "all"
    };
  },
  components: {
    todoInput,
    todoList
  },
  mounted() {
    // setTimeout(() => {
    //   console.log(this.todoById(3));
    // }, 6000);

    this.fetchItems();
  },
  methods: {
    ...mapActions(['fetchItems'])
  },
  computed: {
    ...mapState({
      todos: state => state.todos.todos,
      filter: state => state.todos.filter
    }),
    ...mapGetters(["todoById"]),
    filteredTodos() {
      switch (this.filter) {
        case "all":
          return this.todos;
        case "active":
          return this.todos.filter(item => item.checked === false);
        case "completed":
          return this.todos.filter(item => item.checked);
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.todo {
  margin-top: 100px;
  background: #fff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}
</style>


