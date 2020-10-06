<template>
  <div id="app">
    <form @submit.prevent="onSubmit">
      <input
        class="input"
        type="text"
        placeholder="Добавте новую задачу"
        v-model="curentTaskName"
      />
      <button class="btn" v-if="!isEdit">Добавить</button>
      <button class="btn" v-else>Изменить</button>
    </form>
    <hr />
    <List
      v-bind:tasksList="tasksList"
      @setStatus="setStatus"
      @deleteTask="deleteTask"
      @editTask="editTask"
    />
  </div>
</template>

<script>
import List from "./components/List";
export default {
  name: "App",
  components: {
    List,
  },
  data() {
    return {
      isEdit: false,
      tasksList: [],
      curentTaskName: "",
      curentTaskIndex: -1,
    };
  },
  methods: {
    onSubmit() {
      const taskName = this.curentTaskName.trim();
      if (taskName && !this.isEdit) {
        this.addTask(taskName);
      } else if (this.isEdit && taskName) {
        this.editTaskList(taskName);
        this.setEdit();
      }
      this.clearTaskName();
    },
    setEdit() {
      this.isEdit = false;
    },
    addTask(taskName) {
      const newTask = { id: Date.now(), title: taskName, isComplete: false };
      this.tasksList.push(newTask);
    },
    clearTaskName() {
      this.curentTaskName = "";
    },
    setStatus(index) {
      this.tasksList[index].isComplete = !this.tasksList[index].isComplete;
    },
    deleteTask(taskId) {
      this.tasksList = this.tasksList.filter((e) => e.id !== taskId);
    },
    editTask(index) {
      this.curentTaskName = this.tasksList[index].title;
      this.curentTaskIndex = index;
      this.isEdit = true;
    },
    editTaskList(taskName) {
      if (this.curentTaskIndex !== -1) {
        this.tasksList[this.curentTaskIndex].title = taskName;
        this.curentTaskIndex = -1;
      }
    },
  },
  watch: {
    curentTaskName: function() {
      if (!this.curentTaskName.trim()) {
        this.setEdit();
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: block;
  color: #2c3e50;
  margin: auto;
  padding: 15px;
  margin-top: 60px;
  background: #fff;
  width: 650px;
  box-shadow: 0 0 15px black;
  border-radius: 5px;
}
</style>
