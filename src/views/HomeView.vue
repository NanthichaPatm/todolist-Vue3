<template>
  <div class="home">
    <h1>Todolist</h1>
    <form @submit.prevent="addList">
      <input type="text" v-model="newTodo" placeholder="+add a new todo..." />
      <button type="submit">+</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <div v-if="!todo.edit">
          <input type="checkbox" v-model="todo.done" @change="checkDone()" />
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
          <div class="btn">
            <button @click="editText(index)">
              <BootstrapIcon icon="pencil-square" />
            </button>
            <button @click="removeTodo(index)" class="remove">
              <BootstrapIcon icon="x-square-fill" />
            </button>
          </div>
        </div>
        <div v-else>
          <input class="edit-text" type="text" v-model="todo.text" />
          <div class="btn">
            <button @click="saveEdit(index)">save</button>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
//  JSON.parse(localStorage.getItem('Todos'))
export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      todos: [],
      // [
      //   { text: "doing quiz", done: true, edit: false },
      //   {
      //     text: "say hi dfovjmd hsfdueh  hnoundefvgoeuwdubng ondrgvdeou divj idmejnvn namdv",
      //     done: false,
      //     edit: false,
      //   },
      //   {
      //     text: "say hi",
      //     done: false,
      //     edit: false,
      //   },
      // ],
      newTodo: "",
    };
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },
  watch: {
    todos: {
      handler() {
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
      deep: true,
    },
  },
  methods: {
    addList() {
      this.todos.push({
        text: this.newTodo,
        done: false,
        edit: false,
      });
      this.newTodo = "";
    },
    checkDone() {
      this.todo.done = !this.todo.done;
    },
    editText(i) {
      this.todos[i].edit = true;
    },
    saveEdit(i) {
      this.todos[i].edit = false;
    },
    removeTodo(i) {
      this.todos.splice(i, 1);
    },
  },
};
</script>
<style scoped>
.home {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  border: 1px solid black;
  border-radius: 10px;
  width: 80%;
  margin: 1rem auto;
  font-size: 20px;
}
h1 {
  align-self: center;
  margin-bottom: 5px;
}
form {
  width: 100%;
}
form input {
  padding: 5px 10px;
  margin-bottom: 1rem;
  width: 50%;
  border: none;
  background: rgb(191, 214, 191);
  border-radius: 10px 0px 0px 10px;
  font-size: 15px;
}
form button {
  padding: 5px 10px;
  border: none;
  background: rgb(22, 157, 22);
  border-radius: 0px 10px 10px 0px;
  font-size: 15px;
  color: #fff;
}
ul {
  list-style-type: none;
  width: 50%;
}
li div {
  display: flex;
  justify-content: start;
  align-items: start;
}
li div span {
  padding-left: 10px;
  width: 80%;
  flex-wrap: wrap;
  text-align: start;
}
li div .btn {
  margin-left: auto;
  flex-wrap: wrap;
}
li div input[type="checkbox"],
.btn {
  margin-top: 8px;
}
li div .edit-text {
  font-size: 20px;
  width: 80%;
  border: none;
  background: rgba(181, 194, 181, 0.63);
  border-radius: 5px;
  padding: 5px 10px;
  color: rgb(90, 111, 95);
}
.btn button {
  background: none;
  border: none;
  font-size: 20px;
  color: rgb(47, 81, 47);
  cursor: pointer;
}
.btn .remove:hover {
  color: red;
}
.done {
  text-decoration: line-through;
  color: rgb(158, 180, 163);
}
</style>
