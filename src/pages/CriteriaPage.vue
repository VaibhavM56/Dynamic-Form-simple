<template>
  <q-page class="q-ma-md">
    <h4>Disposition Criteria - Professionalism and Competency</h4>
    <p class="q-ma-sm">
      Please evaluate the CSULB student by checking ONE of the appropriate
      performance expectations or unacceptable behaviors that apply under Met or
      Not Met. Please support the evaluation with comments and/or
      recommendations. "If the CSULB Student does not meet criteria in any of
      the categories, the candidate is required to reflect on Not Met criteria,
      explaining next steps to achieve Met standards by providing a written
      explanation to successfully complete rotation.
    </p>
    <q-card class="form-class q-ma-md">
      <q-markup-table>
        <thead>
          <tr>
            <th class="text-left"></th>
            <th class="text-left">Met(Performance Expectations)</th>
            <th class="text-left">Not Met(Unacceptable Behaviours)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(criteria, index) in criteriaList" :key="index">
            <td>{{ criteria }}</td>
            <td>
              <q-radio v-model="selectedCriteria[index]" val="Met" />
            </td>
            <td>
              <q-radio v-model="selectedCriteria[index]" val="Not Met" />
            </td>
          </tr>
        </tbody>
      </q-markup-table>
    </q-card>
    <div v-if="formattedSelectedCriteria">
      <h4>Generated Schema</h4>
      <pre>{{ formattedSelectedCriteria }}</pre>
    </div>
  </q-page>
</template>

<script setup>
import { ref, computed, watch } from "vue";

const criteriaList = ref([
  "Promptness: Timeliness in first contact: Punctuality in attendance",
  "Responsibility: Consistency in schedule and work",
  "Honoring school setting: Compliance with school policies; Displays legal and ethical conduct; and, observing confidentiality at all times",
  "Representing the university: Respectful in professional language, behavior, and appearance. No use of social media in the schooling context at any time.",
  "Communication Skills: University-level language in email, phone contact, and in person",
  "Working with Diverse Populations: Respect and demonstrates insightfulness for all students, various backgrounds, abilities, and orientations",
  "Collaboration: Willing contribution to classroom environment and learning opportunities",
  "Knowledge: Application of course content and best practices; reflection on learning",
  "OVERALL FINAL EVAULATION",
]);
const selectedCriteria = ref([]);

function log() {
  console.log(selectedCriteria);
}

const formattedSelectedCriteria = computed(() => {
  const schema = {};
  selectedCriteria.value.forEach((value, index) => {
    schema[`Row_${index + 1}`] = value;
  });
  return schema;
});

watch(selectedCriteria, (index) => {});
</script>

<style scoped>
h4 {
  font-size: 2rem;
  font-weight: 350;
}

td {
  border-style: none;
}

th {
  border-style: none;
}
</style>
