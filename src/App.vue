<template>
  <!-- Header -->
  <div class="header">
    <h1>To Do List</h1>
  </div>

  <!-- Form untuk membuat baru -->
  <div class="form">
    <input v-model="newTask" type="text" placeholder="Masukkan Teks">
    <button @click="createTask">Tambahkan Teks</button>
  </div>

  <!-- Daftar tugas -->
  <div class="tasks">
    <ul>
      <li v-for="(task, index) in tasks" :key="index" :class="{ 'done': task.done }">
        <span>{{ task.name }}</span>
        <div>
          <button @click="toggleTaskStatus(task)">{{ task.done ? 'Undo' : 'Done' }}</button>
          <button @click="editTask(task)">Edit</button>
          <button @click="deleteTask(task)">Delete</button>
        </div>
      </li>
    </ul>
  </div>

  <!-- Form untuk edit -->
  <div class="form" v-if="editingTask">
    <input v-model="editingTask.name" type="text" placeholder="Masukkan Teks">
    <button @click="updateTask">Update</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: '',
      editingTask: null
    }
  },
  methods: {
    createTask() {
      if (this.newTask) {
        this.tasks.push({ name: this.newTask, done: false });
        this.newTask = '';
      }
    },
    editTask(task) {
      this.editingTask = task;
    },
    updateTask() {
      this.editingTask = null;
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter(t => t !== task);
    },
    toggleTaskStatus(task) {
      task.done = !task.done;
    }
  }
}
</script>

<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f9f7f7;
  color: #333;
}

.header {
  background-color: #333;
  color: #fff;
  padding: 20px;
  text-align: center;
  border-bottom: 2px solid #333;
}

.form {
  padding: 20px;
  background-color: #f9f7f7;
  border-bottom: 2px solid #333;
}

.form input[type="text"] {
  width: 70%;
  height: 40px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #333;
  border-radius: 5px;
}

.form button {
  height: 40px;
  padding: 0 20px;
  font-size: 16px;
  background-color: #333;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 10px;
}

.form button:hover {
  background-color: #555;
}

.tasks {
  padding: 20px;
}

.tasks ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.tasks li {
  padding: 20px;
  border-bottom: 1px solid #ddd;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.tasks li:last-child {
  border-bottom: none;
}

.tasks button {
  height: 30px;
  padding: 0 10px;
  font-size: 14px;
  background-color: #333;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 5px;
}

.tasks button:hover {
  background-color: #555;
}

.done {
  text-decoration: line-through;
  color: #777;
}
</style>
