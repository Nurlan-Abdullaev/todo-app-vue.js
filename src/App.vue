<template>
  <div id="app">
    <h1>Todo app</h1>
    <div>
      <input v-model="newTask" placeholder="Add a new task" />
      <button @click="addTask">Добавить</button>
    </div>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span :class="{ completed: task.completed }">{{ task.title }}</span>
        <div>
          <input
            type="checkbox"
            v-model="task.completed"
            @input="toggleCompleted(index)"
          />
          <button @click="editTask(index)">edit</button>
          <button @click="removeTask(index)">delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ title: this.newTask.trim(), completed: false });
        this.newTask = "";
        console.log(this.tasks);
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleCompleted(index) {
      console.log("Toggle completed called for index", index);
      if (this.tasks[index]) {
        this.tasks[index].completed = !this.tasks[index].completed;
      }
    },
    editTask(index) {
      const updatedTask = prompt(
        "Введите новое название задачи:",
        this.tasks[index].title
      );
      if (updatedTask !== null) {
        this.tasks[index].title = updatedTask.trim();
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

li {
  margin: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.completed {
  text-decoration: line-through;
}

button {
  margin-left: 5px;
  cursor: pointer;
}
</style>
