<template>
  <div v-if="!postRegistratingMessage">
    <Form @submit="onSubmit" ref="form">
      <Field
        name="First Name"
        type="text"
        placeholder="First Name"
        v-model="firstName"
        :rules="validateFirstName"
      />
      <p><ErrorMessage name="First Name" /></p>

      <Field
        name="Last Name"
        type="text"
        placeholder="Last Name"
        v-model="lastName"
        :rules="validateLastName"
      />
      <p><ErrorMessage name="Last Name" /></p>

      <Field
        name="Email"
        type="email"
        placeholder="Email Address"
        v-model="email"
        :rules="validateEmail"
      />
      <p><ErrorMessage name="Email" /></p>

      <Field
        name="Password"
        type="password"
        placeholder="Password"
        v-model="password"
        :rules="validatePassword"
      />
      <p><ErrorMessage name="Password" /></p>

      <button type="submit">CLAIM YOUR FREE TRIAL</button>
    </Form>
  </div>

  <p v-if="registrationErrorMessage">{{ registrationErrorMessage }}</p>

  <div v-if="postRegistratingMessage">
    <h1>Great! You are now registered</h1>
  </div>
</template>

<script>
import { Field, Form, ErrorMessage } from "vee-validate";
export default {
  name: "App",
  components: { Form, Field, ErrorMessage },
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      password: "",
      postRegistratingMessage: false,
      registrationErrorMessage: "",
    };
  },
  methods: {
    onSubmit() {
      try {
        this.$refs.form.validate().then((success) => {
          if (success) {
            this.postRegistratingMessage = true;
          }
        });
      } catch (error) {
        this.registrationErrorMessage =
          "There was an error submitting the form. Please try again later.";
      }
    },

    validateFirstName(value) {
      if (!value) {
        return "First Name cannot be empty";
      }
      return true;
    },

    validateLastName(value) {
      if (!value) {
        return "Last Name cannot be empty";
      }
      return true;
    },

    validateEmail(value) {
      if (!value) {
        return "Email cannot be empty";
      }
      const regex = /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
      if (!regex.test(value)) {
        return "Looks like this is not an email";
      }
      return true;
    },

    validatePassword(value) {
      if (!value) {
        return "Password cannot be empty";
      }
      const regex =
        /(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[^A-Za-z0-9])(?=.{8,})/;
      if (!regex.test(value)) {
        return "8 Characters long or longer. At least one lowercase letter, one uppercase letter, one digit, or symbol";
      }
      return true;
    },
  },
};
</script>
