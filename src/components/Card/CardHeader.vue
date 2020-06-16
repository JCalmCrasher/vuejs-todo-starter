<template>
  <div class="card-header bg-primary text-white">
    <h4 class="text-center" tabindex="-1" ref="taskTitle">{{ title }}</h4>
  </div>
</template>

<script>
export default {
  props: {
    title: { required: true, type: String }
  }
};
</script>