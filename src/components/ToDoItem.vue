<template>
  <div class="row" v-if="!isEditing">
    <div class="col-6">
      <div class="custom-control custom-checkbox">
        <input
          type="checkbox"
          class="custom-control-input"
          :id="id"
          :checked="isDone"
          @change="$emit('checkbox-changed')"
        />
        <label
          class="custom-control-label"
          :style="{'text-decoration':decoration}"
          :for="id"
          id="lbl-task"
        >{{ label }}</label>
      </div>
    </div>
    <div class="col-6">
      <div class="row">
        <div class="col-12">
          <button
            type="button"
            class="btn btn-primary btn-sm mr-2 mb-2"
            ref="editButton"
            @click="toggleToTaskEditForm"
          >Edit</button>
          <button type="button" class="btn btn-danger btn-sm mb-2" @click="deleteToDo">Delete</button>
        </div>
      </div>
    </div>
  </div>
  <to-do-item-edit-form
    v-else
    :id="id"
    :label="label"
    @task-edited="taskEdited"
    @edit-cancelled="editCancelled"
  ></to-do-item-edit-form>
</template>

<script>
import ToDoItemEditForm from "./ToDoItemEditForm";

export default {
  components: {
    ToDoItemEditForm
  },
  props: {
    label: { required: true, type: String },
    done: { default: false, type: Boolean },
    id: { required: true, type: String },
    decoration: { required: true, type: String }
  },
  data() {
    return {
      isEditing: false
    };
  },
  computed: {
    isDone() {
      return this.done;
    }
  },
  methods: {
    deleteToDo() {
      this.$emit("task-deleted");
    },
    toggleToTaskEditForm() {
      this.isEditing = true;
    },
    taskEdited(newTask) {
      this.$emit("task-edited", newTask);
      this.isEditing = false;
      this.focusOnEditButton();
    },
    editCancelled() {
      this.isEditing = false;
      this.focusOnEditButton();
    },
    focusOnEditButton() {
      this.$nextTick(() => {
        const editButtonRef = this.$refs.editButton;
        editButtonRef.focus();
      });
    }
  }
};
</script>

<style scoped>
#lbl-task,
* {
  font-weight: 500 !important;
}
</style>