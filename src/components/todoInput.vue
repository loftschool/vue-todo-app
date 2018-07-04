<template lang="pug">
  .todo-input
    div.error {{validation.firstError('todo.name')}}
    input(
      type="text"
      placeholder="Todo Name"
      autofocus
      v-model="todo.name"
      :class="{'valid-error' : validation.hasError('todo.name')}"
      @keydown.enter="addNewTodo"
    ).input
</template>
<script>
import { Validator } from "simple-vue-validator";
import { mapMutations } from "vuex";
let uniqId = 0;
export default {
  mixins: [require("simple-vue-validator").mixin],
  validators: {
    "todo.name"(value) {
      return Validator.value(value).required("Поле не может быть пустым");
    }
  },
  data() {
    return {
      todo: {
        id: 0,
        name: "",
        checked: false
      }
    };
  },
  methods: {
    ...mapMutations(['addTodo']),
    addNewTodo() {
      this.$validate().then(success => {
        if (!success) return;

        uniqId++;
        this.todo.id = uniqId;

        this.addTodo({ ...this.todo });

        this.todo.name = "";

        this.validation.reset();
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.input {
  font-size: 24px;
  padding: 16px 16px 16px 60px;
  border: 1px solid transparent;
  background: rgba(0, 0, 0, 0.003);
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
  line-height: 1.4em;
  outline: none;
  color: inherit;
  width: 100%;
  background: #fff;
}

.valid-error {
  border: 1px solid firebrick;
}

.todo-input {
  position: relative;
}

.error {
  position: absolute;
  top: -30px;
  left: 0;
  color: firebrick;
}
</style>

