<template>
  <div>
    <input
      type="text"
      :value="formattedPhone"
      @input="onInput"
      :placeholder="placeholder"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch, computed, onMounted } from "vue";

export default defineComponent({
  name: "PhoneNumberInput",
  props: {
    modelValue: {
      type: String,
      required: true,
    },
  },
  emits: ["update:modelValue"],
  setup(props, { emit }) {
    const formattedPhone = ref("");
    const placeholder = ref("Phone number");

    const formatPhoneNumber = (phone: string) => {
      // Allow only digits, spaces, (, ), -, +
      return phone.replace(/[^0-9\s\(\)\-\+]/g, "");
    };

    const onInput = (event: Event) => {
      const input = event.target as HTMLInputElement;
      const formatted = formatPhoneNumber(input.value);

      console.log(11111, input.value, formatted)

      formattedPhone.value = formatted;
      emit("update:modelValue", formatted);
    };

    const setPlaceholderByLocale = () => {
      const locale = navigator.language || "en";
      if (locale === "en-US") {
        placeholder.value = "+1 (123) 456-7890";
      } else {
        placeholder.value = "Phone number";
      }
    };

    onMounted(() => {
      setPlaceholderByLocale();
    });

    watch(
      () => props.modelValue,
      (newVal) => {
        formattedPhone.value = formatPhoneNumber(newVal);
      }
    );

    return {
      formattedPhone,
      placeholder,
      onInput,
    };
  },
});
</script>

<style scoped></style>
