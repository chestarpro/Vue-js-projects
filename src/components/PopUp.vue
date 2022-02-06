<template>
  <div class="popup-wrapper">
    <div class="block-popup">
      <input type="text" v-model="value" />
      <button
        @click="
          $emit('closeCreateFieldWindow');
          $emit('addField', value);
        "
        class="block-popup__create-btn"
      >
        create
      </button>
      <button
        @click="$emit('closeCreateFieldWindow')"
        class="block-popup__create-btn"
      >
        cancel
      </button>
    </div>
  
  </div>
  
</template>

<script>
export default {
  date() {
    return {
      value: "",
    };
  },
  name: "PopUp",
  props: ["isUpdateFiled"],
};
</script>

<style>
.popup-wrapper {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.2);
  position: absolute;
  top: 0;
  left: 0;
}

.block-popup {
  width: auto;
  height: auto;
  background: #fff;
  align-items: center;
  justify-content: center;
  max-height: 100%;
  background-color: rgba(255, 255, 255, 1);
  padding: 25px;
  border-radius: 25px;
  overflow: auto;
  color: #222;
}

.block-popup input {
  width: 95%;
}
</style>