<script setup>
import { FormKit } from "@formkit/vue";

const handleSubmit = () => {
  console.log("submit");
}
</script>

<template>
  <FormKit type="form" @submit="handleSubmit">
    <FormKit
      type="text"
      name="name"
      id="name"
      label="Message"
      placeholder="“Scarlet Sword”"
    />
  </FormKit>
</template>
