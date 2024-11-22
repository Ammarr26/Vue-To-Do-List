<template>
  <div id="app">
    <header>
      <h1>To Do List</h1>
    </header>
    <main>
      <div class="add-task">
        <input 
          v-model="newTask" 
          @keyup.enter="addTask" 
          type="text" 
          placeholder="Enter a task" />
        <button @click="addTask">Add Task</button>
      </div>
      <ul class="task-list">
        <li v-for="(task, index) in tasks" :key="index">
          <span :class="{ done: task.completed }" @click="toggleTask(index)">
            {{ task.text }}
          </span>
          <button class="delete-btn" @click="deleteTask(index)">X</button>
        </li>
      </ul>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
}
#app {
  max-width: 600px;
  margin: 50px auto;
  padding: 20px;
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
header {
  text-align: center;
  margin-bottom: 20px;
}
header h1 {
  font-size: 24px;
  color: #333;
}
.add-task {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.add-task input {
  flex: 1;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.add-task button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.add-task button:hover {
  background-color: #0056b3;
}
.task-list {
  list-style: none;
  padding: 0;
}
.task-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
}
.task-list li span {
  cursor: pointer;
}
.task-list li span.done {
  text-decoration: line-through;
  color: #888;
}
.delete-btn {
  background-color: red;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}
.delete-btn:hover {
  background-color: darkred;
}
</style>