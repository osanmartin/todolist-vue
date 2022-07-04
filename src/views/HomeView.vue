<template>
  <h1>ToDoList</h1>
  <input type="text" placeholder="Ingresar tarea" v-model="taskNameToAdd" />
  <button type="button" @click="addNewTask">Agregar</button>
  <div>
    <h3>Listado</h3>
    <div class="todo-row" v-for="task of taskList" :key="task.name">
      {{ task.name }}
      <button type="button" @click="deleteTask(task.id)">delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      taskNameToAdd: "",
      taskList: [],
    };
  },
  methods: {
    addNewTask() {
      let newTaskToAdd;
      if (this.taskNameToAdd !== "") {
        newTaskToAdd = {
          id: Math.floor(Math.random() * 100),
          name: this.taskNameToAdd,
        };
        this.taskList = [...this.taskList, newTaskToAdd];
      }
    },
    deleteTask(id) {
      this.taskList = this.taskList.filter((task) => task.id !== id);
    },
  },
  watch: {
    taskList: {
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.taskList));
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      this.taskList = JSON.parse(localStorage.getItem("tasks"));
    } else {
      this.taskList = [];
    }
  },
};
</script>

<style>
.todo-row {
  background-color: gray;
  width: 500px;
  margin: 0 auto;
}
</style>
