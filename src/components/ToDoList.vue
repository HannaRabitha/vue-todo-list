<template>
  <div class="todo-container">
    <h1>Todo List</h1>

    <div class="todo-list-box">
    <div
      v-for="(todo, index) in todos"
      :key="index"
    >

      <div v-if="!editing" class="todo-list flex">
          <div style="width: 80%;"> 
          {{ index + 1 }}. {{ todo.name }} 
          </div>
          <button class="submit-btn" @click="deleteTodo(index)">Hapus</button>
          <button class="submit-btn" @click="editTodo(index)">Edit</button>
      </div>

      <div v-else class="todo-list flex">
          <input style="width: 80%" class="form-control form-input" v-model="changeTodo"/>
          <button class="submit-btn" @click="deleteTodo(index)">Hapus</button>
          <button class="submit-btn" @click="updateTodo(index)">Update</button>
      </div>

      </div>
    </div>

    <!-- <form> -->
      <div class="flex">
      <input
       v-model="newTodo"
        type="text"
        placeholder="Enter To Do"
        class="form-control form-input"
      />
      <button type="submit" class="submit-btn" @click="addTodo()">
        Tambahkan
      </button>
      </div>
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
      changeTodo: "",
      indexEditTodo: null,
      tempNameTodo: "",
      todos: [],
      msg: "",
      editing: false,
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
     editTodo(index) {
      this.editing = true;
      this.changeTodo = this.todos[index].name;
      this.indexEditTodo = index;
    },
    updateTodo() {
      this.editing = false;
      this.todos[this.indexEditTodo].name = this.changeTodo;
      this.indexEditTodo = null;
      
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style scoped>

.flex {
  display: flex;
}

.todo-container {
  text-align: left;
}

.form-input {
  width: 80%;
  border: 1px solid #333;
  padding: 0.5rem 1rem 0.5rem 1rem;
  border-radius: 10px;
}
.form-control:focus {
  box-shadow: none;
  /* border: none; */
}
.submit-btn {
  margin: auto 2rem auto 2rem;
  font-size: 14px;
  color: #333;
}
.todo-list-box {
    margin: auto;
    text-align: left;
} 
.todo-list {
  margin: auto auto 1rem auto;
  display: flex;
  border: 1px;
}
.status-text {
  cursor: pointer;
}
.action-btn i {
  cursor: pointer;
}
.msg {

    margin: 0.5rem auto auto auto;
    text-align: left;
}
</style>