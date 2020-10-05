<template>
  <div>
    <form @submit.prevent="onSubmit">
      <input
        class="input"
        type="text"
        placeholder="Добавте новую задачу"
        v-model="taskName"
      />
      <button class="btn" v-if="!isEdit">Добавить</button>
      <button class="btn" v-else>Изменить</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ["isEdit"],
  data() {
    return {
      taskName: "",
    };
  },
  methods: {
    onSubmit() {
      if (this.taskName.trim() && !this.isEdit) {
        this.$emit("addTask", this.taskName);
      } else if (this.isEdit && this.taskName.trim()) {
        this.$emit("editTask", this.taskName);
        this.$emit("setEdit");
      }
      this.taskName = "";
    },
  },
  watch: {
    taskName: function() {
      if (!this.taskName.trim()) {
        this.$emit("setEditFalse");
      }
    },
  },
};
</script>
