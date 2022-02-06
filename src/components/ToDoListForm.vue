<template>
  <div class="app-container">
    <h1 class="app-header">Vue TO DO LIST</h1>
    <ToDoListField
      v-bind:taskItem="taskItem"
      @createNewItem="createNewItem"
      @openCreateFieldWindow="isUpdateFieldWindow(true)"
    />
    <ul class="task-list">
      <ToDoListItem
        v-for="(task, index) in tasks"
        :key="task + index"
        v-bind:task="task"
        v-bind:index="index"
        v-bind:tasks="tasks"
        @deleteItem="deleteItem(task)"
        @setTaskDone="setTaskDone(index)"
        @updateItem="updateItem(index)"
      />
    </ul>
    <PopUp
      v-if="isUpdateFiled"
      v-bind:isUpdateFiled="isUpdateFiled"
      @closeCreateFieldWindow="isUpdateFieldWindow(false)"
      @addField="addField(value)"
    />
  </div>
</template>

<script>
import ToDoListItem from "./ToDoListItem.vue";
import ToDoListField from "./ToDoListField.vue";
import PopUp from "./PopUp.vue";

export default {
  components: {
    ToDoListItem,
    ToDoListField,
    PopUp,
  },
  data() {
    return {
      title: "to do list",
      fieldValue: "",
      isUpdateFiled: false,
      taskItem: {
        fields: {
          title: "",
          description: "",
        },
        createDate: new Date().toISOString().split("T")[0],
        createDateTime: new Date().toISOString().split("T")[1].slice(0, 8),
        updateDate: new Date().toISOString().split("T")[0],
        updateDateTime: new Date().toISOString().split("T")[1].slice(0, 8),
        isDone: false,
        isUpdate: false,
      },
      tasks: localStorage.getItem("tasks")
        ? JSON.parse(localStorage.getItem("tasks"))
        : [],
    };
  },
  methods: {
    isUpdateFieldWindow(value) {
      this.isUpdateFiled = value;
    },
    createNewItem: function () {
      if (!this.taskItem.fields.title) {
        alert("Title is empty");
        return;
      }
      this.tasks.push({ ...this.taskItem });

      localStorage.setItem("tasks", JSON.stringify(this.tasks));
      for (const field of this.taskItem.fields) {
        this.taskItem.fields[field] = "";
      }
    },
    addField(value) {
      if (value === '') alert("Error");
      else {
        this.$set(this.taskItem.fields,value, "");
        value = '';
      }
    },
    setTaskDone(index) {
      this.tasks[index].isDone = !this.tasks[index].isDone;
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },

    deleteItem(task) {
      console.log(task);
      this.tasks.splice(this.tasks.indexOf(task), 1);
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    updateItem(index) {
      this.tasks[index].isUpdate = false;
      if (
        this.tasks[index].title === "" &&
        this.tasks[index].description === ""
      ) {
        this.deleteItem(index);
      } else {
        (this.tasks[index].updateDate = new Date().toISOString().split("T")[0]),
          (this.tasks[index].updateDateTime = new Date()
            .toISOString()
            .split("T")[1]
            .slice(0, 8)),
          localStorage.setItem("tasks", JSON.stringify(this.tasks));
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=DM+Sans:400,500,700&display=swap");
* {
  box-sizing: border-box;
}

:root {
  --checkbox-color: rgb(202, 60, 60);
  --checkbox-shadow: rgba(238, 156, 167, 0.2);
  --add-button: rgba(255, 255, 255, 0.7);
  --add-button-shadow: rgba(238, 156, 167, 0.4);
}

.app-container {
  margin: 0 auto;
  margin-top: 200px;
  max-width: 600px;
  width: 100%;
  max-height: 100%;
  background-color: rgba(255, 255, 255, 0.3);
  padding: 25px;
  border-radius: 25px;
  overflow: auto;
  color: #222;
}

.app-header {
  font-size: 20px;
  line-height: 32px;
  margin: 0 0 12px 0;
  color: #272727;
}
</style>