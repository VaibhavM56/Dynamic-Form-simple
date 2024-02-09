<template>
  <div class="draggable-field" draggable="true" @dragstart="dragStart">
    {{ label }}
  </div>
</template>

<script>
export default {
  props: ["label"],
  methods: {
    dragStart(event) {
      event.dataTransfer.setData("text/plain", this.label);
    },
  },
};
</script>
