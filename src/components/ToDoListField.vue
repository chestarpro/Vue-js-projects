<template>
  <div>
    <input
      class="submit-add-field"
      type="button"
      value=""
      title="Add field"
      @click="$emit('openCreateFieldWindow')"
    />
    <input
      class="field"
      :class="fieldType === 'title' ? 'title' : 'field'"
      type="text"
      :placeholder="fieldType"
      :key="fieldType"
      v-for="(field, fieldType) in taskItem.fields"
    />

    <input
      class="submit-add-task"
      type="button"
      value=""
      title="Add task"
      @click="$emit('createNewItem')"
    />
  </div>
</template>

<script>
export default {
  name: "ToDoListField",
  props: ["taskItem"],
};
</script>

<style>
input {
  outline: none;
}
.submit-add-field {
  float: right;
  margin-top: -40px;
  width: 32px;
  height: 32px;
  border: none;
  background: var(--add-button);
  background-image: url(../assets/addField.png);
  background-size: 32px;
  cursor: pointer;
}

.submit-add-task {
  float: right;
  margin-right: 5px;
  margin-top: -10px;
  width: 32px;
  height: 32px;
  flex-shrink: 0;
  border: none;
  background: var(--add-button);
  color: #272727;
  background-image: url(../assets/add.png);
  background-size: 32px;
  background-position: center;
  background-repeat: no-repeat;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 0 12px 0 var(--add-button-shadow);
}

.add-task {
  height: 40px;
  font-size: 14px;
  display: flex;
}

.field {
  display: block;
  width: 80%;
  margin-top: 15px;
  height: 20px;
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

.title {
  display: block;
  width: 40%;
  margin-top: 15px;
  height: 20px;
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
</style>