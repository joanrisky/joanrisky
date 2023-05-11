<template>
  <div class="todo-list">
    <h1>Rutinitas Shalat</h1>
      <form @submit.prevent="addTodo">
        <input type="text" v-model="newTodo" placeholder="Tambahkan.."/>
        <button type="submit" class="tambahkan">Tambah</button>
      </form>
      <h2>Daftar Shalat</h2>
      <div class="tengah">
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.done"/>
          <span :class="{ 'done': todo.done }">{{ todo.text }}</span>
          <button @click="removeTodo(index)">Hapus</button>
        </li>
      </ul>
    
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return
      }
      this.todos.push({
        text: this.newTodo,
        done: false
      })
      this.newTodo = ''
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    showAll() {
      this.filter = 'all'
    },
    showActive() {
      this.filter = 'active'
    },
    showCompleted() {
      this.filter = 'completed'
    }
  },
  computed: {
    filteredTodos() {
      switch (this.filter) {
        case 'active':
          return this.todos.filter(todo => !todo.done)
        case 'completed':
          return this.todos.filter(todo => todo.done)
        default:
          return this.todos
      }
    }
  }
}
</script>

<style>

body{
background-color: #0099FF; 
}
.todo-list {
  max-width: px;
  margin: 0 auto;
  padding: 40px;
  font-size: 1.2rem;
  background-color: #0099FF;
}

.todo-list h1 {
  text-align: center;
  color: white;
}

.todo-list form {
    display: flex;
    margin-bottom: 20px;
}

.todo-list input[type=text] {
    flex: 0.4;
    margin-left: 110px;
    padding: 2px;
    font-size: 01.2rem;
    border-radius: 10px;
}

.todo-list button[type=submit] {
    margin-left: 10px;
    padding: 8px;
    font-size: 1.2rem;
    background-color: blue;
    border-radius: 9910px;
}

.todo-list h2{
  text-align: center;
  color: white;
}

.todo-list ul {
    list-style: none;
    padding: 0;
    font-size: 1.9rem;
}

.todo-list li {
    display: flex;
    align-items:center;
    margin-bottom: 10px;
}

.todo-list input[type=checkbox] {
    margin-right: 30px;
}

.todo-list .done {
    text-decoration: line-through;
    color: black;
}

.todo-list button {
    margin-left: 10px;
    padding: 8px;
    background-color: blue;
    border: none;
    cursor: pointer;
    font-size: 1.2rem;
    color: #fff;
    border-radius: 10px;
}

.tengah{
  margin-left: 42%;

}



</style>