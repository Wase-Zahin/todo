<template>
  <form v-if="formDisplay" @submit.prevent="onSubmit">
    <label for="new-todo-input"></label>
    <input type="text" id="new-todo-input" name="new-todo" autocomplete="off" v-model.lazy.trim="label" />
    <div class="btnDiv">
      <button class="addBtn" type="submit">Add</button>
      <button class="cancelBtn" type="button" @click="formDisplay = false">Cancel</button>
    </div>
  </form>
  <button v-else class="addTaskBtn" type="button" @click="formDisplay = true">Add Task +</button>
</template>

<script>
export default {
  data() {
    return {
      label: "",
      formDisplay: false,
      btnDisplay: false,
    }
  },
  methods: {
    onSubmit() {
      if (this.label === '') return;
      this.$emit("todo-added", this.label);
      this.label = "";
      this.formDisplay = false;
    },
    addComponent() {
      this.formDisplay = true;
    }
  }
}

</script>
