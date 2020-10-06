<template>
  <div id="app">
    <Form v-bind:isEdit="isEdit" @setEdit="setEdit" @addTask="addTask" />
    <hr />
    <List
      v-bind:tasksList="tasksList"
      @setStatus="setStatus"
      @deleteTask="deleteTask"
    />
  </div>
</template>

<script>
import Form from "./components/Form";
import List from "./components/List";
export default {
  name: "App",
  components: {
    Form,
    List,
  },
  data() {
    return {
      isEdit: false,
      tasksList: [],
    };
  },
  methods: {
    setEdit() {
      this.isEdit = false;
    },
    addTask(taskName) {
      const newTask = { id: Date.now(), title: taskName, isComplete: false };
      this.tasksList.push(newTask);
    },
    setStatus(index) {
      this.tasksList[index].isComplete = !this.tasksList[index].isComplete;
    },
    deleteTask(taskId) {
      this.tasksList = this.tasksList.filter((e) => e.id !== taskId);
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
