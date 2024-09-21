<template>
  <div id="app">
    <div class="container">
      <h1>My Strawberry Notes</h1>
      <div class="input-container">
        <input
          v-model="newTask"
          placeholder="Adicione uma nova tarefa"
          class="task-input"
        />
        <button @click="addTask" class="add-btn">Adicionar</button>
      </div>
      <ul>
        <li v-for="task in tasks" :key="task.id" :class="{ completed: task.completed }">
          <input
            type="checkbox"
            v-model="task.completed"
            class="checkbox"
          />
          <span class="task-text">{{ task.text }}</span>
          <button @click="editTask(task)" class="btn edit-btn">Editar</button>
          <button @click="removeTask(task.id)" class="btn remove-btn">Remover</button>
        </li>
      </ul>
    </div>
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
      if (this.newTask.trim() === '') return;

      this.tasks.push({
        id: Date.now(), 
        text: this.newTask,
        completed: false
      });
      this.newTask = '';
    },
    removeTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
    },
    editTask(task) {
      const newText = prompt('Edite a tarefa:', task.text);
      if (newText !== null && newText.trim() !== '') {
        task.text = newText;
      }
    }
  }
};
</script>

<style scoped>
:root {
  --primary-color: #ffb3ba;
  --secondary-color: #ebbee3; 
  --accent-color: #bae1ff;
  --text-color: #ffffff;
  --background-color: #f0f4f8;
}

body {
  background-color: #a55c62;
  color: var(--text-color);
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh; 
  background-color: #ffffff;
}

.container {
  max-width: 600px;
  width: 100%;
  padding: 20px;
  background: url('assets/background.jpg'); 
  background-size: cover;
  background-position: center;
  border-radius: 10px;
  box-shadow: 0 4px 16px rgba(202, 83, 123, 0.562);
}

h1 {
  margin-bottom: 20px;
  color: #fd5f79;
  text-align: center;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
}

.task-input {
  flex: 1;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 5px;
  background-color: #ffffff; 
  color: var(--text-color);
  transition: border 0.3s;
}

.task-input:focus {
  border-color: #fd5f79;
}

.add-btn {
  padding: 10px 15px;
  background-color: #ff7c92;
  color: #ffffff;
  border: none;
  border-radius: 5px;
  margin-left: 10px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s;
}

.add-btn:hover {
  background-color: #fd5f79;
  transform: scale(1.05);
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 10px;
  background-color: #ffffff;
  border: 2px solid #fabac5;
  transition: background-color 0.3s, transform 0.3s;
}

li:hover {
  background-color: #faf0f3;
  transform: scale(1.02);
}

.checkbox {
  margin-right: 10px;
  cursor: pointer;
}

.checkbox:checked {
  accent-color: #ff7c92;
}

.task-text {
  flex: 1;
  color: var(--text-color);
}

.completed .task-text {
  text-decoration: line-through;
  color: #aaa;
}

.btn {
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s;
}

.btn:hover {
  transform: translateY(-2px);
}

.edit-btn {
  margin-right: 10px;
  background-color: #74a122; 
  color: white;
}

.edit-btn:hover {
  background-color: #5e8516; 
}

.remove-btn {
  background-color: #f55e5e; 
  color: #fff;
}

.remove-btn:hover {
  background-color: #e45353;
}
</style>
