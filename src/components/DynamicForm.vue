<template>
  <div class="form-builder">
    <q-card class="draggable-container">
      <draggable-field
        v-for="field in draggableFields"
        :key="field.label"
        :label="field.label"
      />
    </q-card>
  </div>

  <br />
  <br />
  <div>
    <q-card class="form-container" @drop="dropField" @dragover.prevent>
      <q-input
        outlined
        v-for="(field, index) in formFields"
        :key="index"
        :placeholder="field.label"
        :class="{ 'invalid-input': field.error }"
        v-model="field.value"
      >
        <template v-slot:after>
          <q-btn round dense flat icon="delete" @click="removeField()" />
        </template>
      </q-input>
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
    removeField(index) {
      this.formFields.splice(index, 1);
    },
  },
};
</script>

<style>
.form-builder {
  display: flex;
  justify-content: space-around;
}

.draggable-container {
  width: 250px;
  margin: 10px 35px 10px 10px;
  padding: 10px;
}

.form-container {
  width: 100%;
  height: 40%;
  flex: 1;
  padding: 80px;
  border: 1px #ccc;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.invalid-input {
  border: 1px solid red;
  padding: 10px;
}
</style>
