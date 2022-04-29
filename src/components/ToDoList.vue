<template>
  <div>
    <h1>Latihan Vue CLI</h1>

    <div class="todo-list-box">
     <div
      class="todo-list"
      v-for="(todo, index) in todos"
      :key="index"
    >
          <div class="status-text">
           <h5>
          {{ index + 1 }}. {{ todo.name }} 
          </h5>
          </div>
    </div>
    </div>

    <!-- <form> -->
      <input
        v-model="newTodo"
        type="text"
        placeholder="Enter To Do"
        class="form-control form-input"
      />
      <button type="submit" class="submit-btn" @click="addTodo()">
        Tambahkan
      </button>
    <!-- </form> -->

    <div class="msg">{{ msg }}</div>
   
  </div>
</template>
    
<script>
export default {
  name: "ToDoList",

  data() {
    return {
      newTodo: "",
      indexEditTodo: null,
      tempNameTodo: "",
      todos: [],
      msg: "",
    };
  },

  methods: {
    addTodo() {
      if (this.newTodo.length === 0) return;

      if (this.indexEditTodo === null) {
        this.todos.push({
          name: this.newTodo,
        });
      } else {
        this.todos[this.indexEditTodo].name = this.newTodo;
        this.indexEditTodo = null;
      }

     if (this.todos.length === 4 || this.todos.length >= 4) {
         this.msg = "Hebat!"
     } else {
         this.msg = ""
     }

      this.newTodo = "";
    },

  },
};
</script>

<style scoped>
.form-input {
  border: 1px solid #333;
  margin-right: 0.5rem;
  padding: 0.5rem 1rem 0.5rem 1rem;
  border-radius: 10px;
}
.form-control:focus {
  box-shadow: none;
  /* border: none; */
}
.submit-btn {
  font-size: 14px;
  color: #333;
}
.todo-list-box {
    width: 15rem;
    margin: auto;
    text-align: left;
}
.todo-list {
 border: 1px;
}
.status-text {
  cursor: pointer;
}
.action-btn i {
  cursor: pointer;
}
.msg {
    width: 15rem;
    margin: 0.5rem auto auto auto;
    text-align: left;
}
</style>