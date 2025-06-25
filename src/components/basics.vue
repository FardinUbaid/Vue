<template>
  <div>
    <h1>Vue App</h1>
    <h2>Count: {{ count }}</h2>

    <button @click="increment">➕ Increase</button>
    <button @click="decrement">➖ Decrease</button>
    <button @click="reset">Reset</button>
    <p>Count is: {{ evenOrOdd }}</p>

    <p v-if="count === 0">You're at zero. Zen mode. 🧘</p>
    <p v-else-if="count > 0">You're above zero. Sky high! 🚀</p>
    <p v-else>In the negatives. Yikes! ❄️</p>

    <hr />
    <h1>First Reverse Operation</h1>
    <input v-model="str" placeholder="Type your name here..." />
    <h1>{{ reverseStr }}</h1>

    <hr />
    <h1>First char counts</h1>

    <input v-model="str2" placeholder="Type something..." />
    <p v-if="countChars > 10">Whoa too many chars babyBro!</p>

    <hr />
    <h1>Baby's To Do List</h1>
    <input v-model="Newtask" placeholder="Add a task..." />
    <button @click="addTodo">Add Task</button>

    <!-- <ul>
      <li v-for="(task, index) in todoList" :key="index">
        {{ task }}
        <button @click="removeTodo(index)">❌</button>
      </li>
    </ul> -->

    <table class="todo-table">
      <tr v-for="(task, index) in todoList" :key="index">
        <td class="task-cell">
          <template v-if="editingIndex === index">
            <input v-model="editingText" class="edit-input" />
          </template>
          <template v-else>
            {{ task }}
          </template>
        </td>
        <td class="button-cell">
          <template v-if="editingIndex === index">
            <button @click="saveEdit(index)">💾 Save</button>
            <button @click="cancelEdit">❌ Cancel</button>
          </template>
          <template v-else>
            <button @click="editTodo(index)">✏️ Edit</button>
            <button @click="removeTodo(index)">❌</button>
          </template>
        </td>
      </tr>
    </table>

    <hr />
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      count: 0,
      str: "",
      str2: "",
      Newtask: "",
      todoList: [],
      editingIndex: null,
      editingText: "",
    };
  },

  methods: {
    increment() {
      this.count++;
    },
    decrement() {
      this.count--;
    },
    reset() {
      this.count = 0;
    },
    addTodo() {
      if (this.Newtask.trim() !== "") {
        this.todoList.push(this.Newtask.trim());
        this.Newtask = "";
      }
    },
    removeTodo(index) {
      this.todoList.splice(index, 1);
    },
    editTodo(index) {
      this.editingIndex = index;
      this.editingText = this.todoList[index];
    },
    saveEdit(index) {
      if (this.editingText.trim() !== "") {
        this.todoList[index] = this.editingText.trim();
        this.cancelEdit();
      }
    },
    cancelEdit() {
      this.editingIndex = null;
      this.editingText = "";
    },
  },

  computed: {
    evenOrOdd() {
      return this.count % 2 === 0 ? "Even" : "Odd";
    },
    reverseStr() {
      return this.str.split("").reverse().join("");
    },
    countChars() {
      return this.str2.length;
    },
  },
};
</script>
<style>
input {
  padding: 10px;
  border-radius: 10px;
  border: 2px solid #333;
  margin-bottom: 10px;
  width: 50%;
  vertical-align: middle;
}
.todo-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 8px;
  margin-top: 10px;
}
.task-cell {
  text-align: left;
  padding: 8px 12px;
  width: 70%;
  word-break: break-word;
}
.button-cell {
  text-align: right;
  padding: 8px 12px;
  vertical-align: middle;
  width: 30%;
  min-width: 160px;
  white-space: nowrap;
}
.edit-input {
  width: 90%;
  padding: 6px;
  vertical-align: middle;
  padding: 10px;
  border-radius: 10px;
  border: 2px solid #333;
}
td input {
  width: 100%;
  box-sizing: border-box;
  vertical-align: middle;
}
</style>
