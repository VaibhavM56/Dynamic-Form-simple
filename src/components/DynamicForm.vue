<template>
  <div class="form-builder">
    <q-card class="draggable-container">
      <draggable-field
        v-for="field in draggableFields"
        :key="field.label"
        :label="field.label"
      />
    </q-card>
    <q-card class="form-container" @drop="dropField" @dragover.prevent>
      <q-input
        outlined
        v-for="(field, index) in formFields"
        :key="index"
        :placeholder="field.label"
        :class="{ 'invalid-input': field.error }"
        v-model="field.value"
      />
    </q-card>
  </div>
</template>

<script>
import DraggableField from "./DraggableField.vue";

export default {
  components: {
    DraggableField,
  },
  data() {
    return {
      draggableFields: [
        { label: "Text Field", type: "text" },
        { label: "Email Field", type: "email" },
        { label: "Phone Number Field", type: "integer" },
        // { label: 'Number Field' },
        // Add more field types as needed
      ],
      formFields: [],
    };
  },
  methods: {
    dropField(event) {
      const label = event.dataTransfer.getData("text/plain");
      if (label) {
        this.formFields.push({ label, value: "", error: "" });
      }
    },
  },
};
</script>

<style>
.form-builder {
  display: flex;
}

.draggable-container {
  width: 200px;
}

.form-container {
  flex: 1;
  padding: 20px;
  border: 1px dashed #ccc;
}

.invalid-input {
  border: 1px solid red;
}
</style>
