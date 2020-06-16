<template>
  <form class="mb-3" @submit.prevent="onSubmit">
    <div>
      <label class="edit-label">Edit Name for &quot;{{label}}&quot;</label>
      <input
        :id="id"
        type="text"
        autocomplete="off"
        v-model.lazy.trim="newLabel"
        class="form-control mb-1"
        ref="labelInput"
      />
    </div>
    <div class="btn-group">
      <button type="button" class="btn btn-dark" @click="onCancel">Cancel</button>
      <button type="submit" class="btn btn-success ml-2">Save</button>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      newLabel: this.label
    };
  },
  methods: {
    onSubmit() {
      if (this.newLabel && this.newLabel !== this.label) {
        this.$emit("task-edited", this.newLabel);
      }
    },
    onCancel() {
      this.$emit("edit-cancelled");
    },
    mounted() {
      const labelInputRef = this.$refs.labelInput;
      labelInputRef.focus();
    }
  }
};
</script>