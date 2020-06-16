<template>
  <div class="row mb-3">
    <div class="col-12">
      <form @submit.prevent="onSubmit">
        <div class="row">
          <div class="col-6">
            <label for="new-todo-input" class="text-center">What needs to be done?</label>
            <input
              type="text"
              id="new-todo-input"
              name="new-todo"
              class="form-control"
              v-model.lazy.trim="label"
              autocomplete="off"
            />
          </div>
          <div class="col-6"><br>
            <button type="submit" class="btn btn-primary btn-block mt-2">Add Task</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onSubmit() {
      if (this.label === "") {
        this.error = "Cannot add empty task";
        return false;
      }

      this.$emit("add-todo", this.label);
      this.error = "";
      this.label = "";
    }
  },
  data() {
    return {
      label: "",
      error: ""
    };
  }
};
</script>