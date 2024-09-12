<template>
  <div>
    <h1>Phone Number Input Demo</h1>
    <PhoneNumberInput v-model="phoneNumber" />
    <p>Entered Phone Number: {{ phoneNumber }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import PhoneNumberInput from "~/components/PhoneNumberInput.vue";

export default defineComponent({
  components: {
    PhoneNumberInput,
  },
  setup() {
    const phoneNumber = ref("");

    return {
      phoneNumber,
    };
  },
});
</script>

<style scoped>
</style>
