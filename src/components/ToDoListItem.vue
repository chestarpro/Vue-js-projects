<template>
  <li>
    <span class="task-date">
      Create date: {{ task.createDate }} {{ task.createDateTime }} &nbsp; |
      &nbsp; Update date: {{ task.updateDate }} {{ task.updateDateTime }}
    </span>
    <div class="task-list-item">
      <label class="task-list-item-label">
        <input
          v-if="!task.isUpdate"
          type="checkbox"
          class="isDone"
          :class="{ active: task.isDone }"
          @click="$emit('setTaskDone', index)"
        />

        <div v-for="(fieldVal, fieldType) in task.fields" :key="fieldType" class="block"> 
       <span v-if="!task.isUpdate" v-bind:class="{ lineThrough: task.isDone}"> 
        {{fieldType}}: {{task.fields[fieldType]}} &nbsp; 
       </span> 
 
     </div>
        <input
          v-if="task.isUpdate"
          class="title-input-upadte"
          type="text"
          autocomplete="off"
          placeholder="Title"
          v-model="task.title"
        />
        <input
          v-if="task.isUpdate"
          class="description-input-upadte"
          type="text"
          autocomplete="off"
          placeholder="Description"
          v-model="task.description"
        />
      </label>
      <span
        class="update-btn"
        title="Update Task"
        v-if="task.isUpdate"
        @click="$emit('updateItem', index)"
        >{{ task.del }}</span
      >
      <span
        class="edit-btn"
        title="Edit Task"
        task.isUpdate
        v-if="!task.isUpdate"
        @click="task.isUpdate = true"
        >{{ task.del }}</span
      >
      <span
        class="delete-btn"
        title="Delete Task"
        @click="$emit('deleteItem', task)"
      ></span>
    </div>
  </li>
</template>

<script>
export default {
  name: "ToDoListItem",
  props: ["task", "tasks", "index"],
};
</script>

<style>

.task-date {
  margin-left: 10px;
  font-size: 12px;
}

ul {
  list-style: none;
  padding: 0;
}

.title-input-upadte {
  width: 40%;
  padding: 0 5px;
  outline: none;
  border: none;
  border-bottom: 1px solid #272727;
  background-color: transparent;
  margin-right: 15px;
  color: #272727;
  box-shadow: none;
  border-radius: 0;
}

.description-input-upadte {
  width: 70%;
  padding: 0 5px;
  outline: none;
  border: none;
  border-bottom: 1px solid #272727;
  background-color: transparent;
  margin-right: 15px;
  color: #272727;
  box-shadow: none;
  border-radius: 0;
}

.task-list-item {
  background-color: rgba(255, 255, 255, 0.7);
  display: flex;

  align-items: center;
  padding: 8px;
  border-radius: 35px;
  margin-bottom: 12px;
}

.isDone {
  width: 16px;
  height: 16px;
  border: 1px solid #272727;
  border-radius: 50%;
  background-image: url(../assets/checked.png);
  background-repeat: no-repeat;
  background-position: center;
  background-size: 0;
  transition: 0.2s;
  margin-right: 8px;
  flex-shrink: 0;
  margin-top: 4px;
  appearance: none;
}

.task-list-item input:hover {
  border-color: var(--checkbox-color);
  box-shadow: 0 0 0 3px var(--checkbox-shadow);
}
.active {
  background-size: 16px;
  border: 1px solid var(--checkbox-color);
  background-color: var(--checkbox-color);
}

.lineThrough {
  color: #272727;
  text-decoration: line-through #272727;
}

.task-list-item-label {
  display: flex;
  align-items: flex-start;
  color: #272727;
  margin-right: 8px;
  font-size: 14px;
  line-height: 24px;
  position: relative;
  transition: 0.2s;
  cursor: pointer;
}

.delete-btn {
  width: 24px;
  height: 24px;
  background-image: url(../assets/delete.png);
  background-repeat: no-repeat;
  background-size: 24px;
  background-position: center;
  cursor: pointer;
}

.edit-btn {
  margin-left: auto;
  margin-right: 5px;
  display: block;
  width: 22px;
  height: 22px;
  background-image: url(../assets/edit.png);
  background-repeat: no-repeat;
  background-size: 22px;
  background-position: center;
  cursor: pointer;
}

.update-btn {
  margin-left: auto;
  margin-right: 5px;
  display: block;
  width: 24px;
  height: 24px;
  background-image: url(../assets/update.png);
  background-repeat: no-repeat;
  background-size: 24px;
  background-position: center;
  cursor: pointer;
}
</style>