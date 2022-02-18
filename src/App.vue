<template>
  <div id="app">
    <header>
      <h1 class="title">to do list</h1>
    </header>

    <div class="add-todo-wrapper">
      <div class="input-wrapper">
        <input
          ref="todo"
          v-model="todo"
          type="text"
          placeholder="Введите задачу"
        />
      </div>
      <div class="button-wrapper">
        <button @click="addTodo">Добавить</button>
      </div>
    </div>

    <div class="subtitle">
      <h2 class="subtitle__objective">Задачи:</h2>
    </div>

    <div class="todos-wrapper">
      <Todo
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @remove-todo="onRemoveTodo(index)"
        @end-edit="onEndEditTodo"
      />
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo.vue";
export default {
  components: {
    Todo,
  },
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (!this.todo) {
        return;
      }

      let now = new Date().toLocaleString();

      this.todos.push({
        dates: now,
        text: this.todo,
      });

      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.todo = "";
    },
    onRemoveTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    onEndEditTodo() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  mounted() {
    const data = localStorage.getItem("todos");
    if (data) {
      this.todos = JSON.parse(data);
    }
    this.$refs.todo.focus();
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.title {
  text-align: center;
  margin-top: 20px;
  font-family: "Montserrat";
  font-weight: bold;
  font-size: 36px;
  line-height: 44px;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: #0e5582;
}
.add-todo-wrapper {
  display: flex;
  width: 482px;
  height: 96px;
  margin: 0 auto;
  margin-top: 40px;
  background: #ffffff;
  border-radius: 5px;
  padding: 30px 25px;
  box-shadow: 4px 4px 12px 2px rgba(0, 0, 0, 0.19);
  -webkit-box-shadow: 4px 4px 12px 2px rgba(0, 0, 0, 0.19);
  -moz-box-shadow: 4px 4px 12px 2px rgba(0, 0, 0, 0.19);
}
.input-wrapper {
  width: 294px;
  height: 36px;
  border: 2px solid #4faed5;
  box-sizing: border-box;
  border-radius: 5px;
}
.input-wrapper input {
  width: 100%;
  height: 100%;
  padding-left: 14px;
  font-family: "Roboto";
}
.button-wrapper {
  width: 105px;
  height: 36px;
  margin-left: 33px;
}
.button-wrapper button {
  width: 100%;
  height: 100%;
  background: #62abd9;
  border-radius: 5px;
  font-family: "Roboto";
  font-size: 18px;
  line-height: 21px;
  color: #ffffff;
  cursor: pointer;
}
.subtitle {
  margin: 0 auto;
  margin-top: 30px;
  width: 90px;
   &__objective{
   margin: 0 auto;
  font-family: "Roboto";
  font-size: 24px;
  line-height: 28px;
  color: #ffffff;
  text-transform: capitalize;
   }
}

.todos-wrapper {
  display: flex;
  flex-direction: column;
  width: 700px;
  margin: 0 auto;
  margin-top: 30px;
  background: #ffffff;
  border-radius: 5px;
}
@media screen and (max-width: 768px) {
.todos-wrapper {
  width: 557px;
}
}
/*0px - 576px*/
@media screen and (max-width: 576px) {
   .add-todo-wrapper {
  width: 95%;
    height: 86px;
    padding: 25px 15px;
}
.input-wrapper {
  width: 80%;
}
.button-wrapper {
  width: 95px;
  margin-left: 15px;
}
.button-wrapper button {
  font-size: 14px;
}
.todos-wrapper {
  width: 95%;
}
}
</style>
