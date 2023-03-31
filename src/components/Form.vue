<template>
  <Form @submit="onSubmit">
    <Input
      label="First Name"
      type="text"
      placeholder="First Name"
      v-model="firstName"
    />
    <Input
      label="Last Name"
      type="text"
      placeholder="Last Name"
      v-model="lastName"
    />
    <Input
      label="Email"
      type="email"
      placeholder="Email Address"
      v-model="email"
    />
    <Input
      label="Password"
      type="password"
      placeholder="Password"
      v-model="password"
    />
    <button>CLAIM YOUR FREE TRIAL</button>
  </Form>
</template>

<script>
import { Input } from "./Input.vue";
import { Form } from "vee-validate";
export default {
  name: "App",
  components: { Input, Form },
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      password: "",
    };
  },
  methods: {
    onSubmit(values) {
      console.log(values);
    },
  },
};
</script>

<style></style>
