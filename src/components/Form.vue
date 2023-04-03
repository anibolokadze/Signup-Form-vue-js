<template>
  <main>
    <div v-if="!postRegistratingMessage" class="flex">
      <div class="info-wrapper">
        <h1>Learn to code by watching others</h1>
        <p>
          See how experienced developers solve problems in real-time. Watching
          scripted tutorials is great, but understanding how developers think is
          invaluable.
        </p>
      </div>
      <div class="form-wrapper">
        <div class="sale-wrapper">
          <h2>Try it free 7 days then</h2>
          <p>$20/mo. thereafter</p>
        </div>
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
          <div class="terms">
            <p>By clicking the button, you are agreeing to our</p>
            <span>Terms and Services</span>
          </div>
        </Form>
      </div>
    </div>

    <p v-if="registrationErrorMessage">{{ registrationErrorMessage }}</p>
  </main>

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

<style lang="scss">
$Red: hsl(0, 100%, 74%);
$Green: hsl(154, 59%, 51%);
$Green-Hover: hsla(154, 65%, 68%, 1);
$Blue: hsl(248, 32%, 49%);
$Dark-Blue: hsl(249, 10%, 26%);
$Grayish-Blue: hsl(246, 25%, 77%);

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
  color: white;
  text-align: center;
}
body {
  background: $Red;
  margin: 0 24px;
  padding: 88px 0;
  .flex {
    background-image: url("../assets/bg-intro-mobile.png");
  }
}
h1 {
  font-size: 28px;
  margin-bottom: 16px;
}
p {
  font-weight: 500;
  font-size: 16px;
}
.info-wrapper {
  p {
    margin-bottom: 64px;
  }
}
.sale-wrapper {
  height: 88px;
  background: $Blue;
  box-shadow: 0px 8px 0px rgba(0, 0, 0, 0.14688);
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  h2 {
    font-size: 15px;
  }
}
.input--error {
  border-color: red;
}
Form {
  background: white;
  box-shadow: 0px 8px 0px rgba(0, 0, 0, 0.14688);
  border-radius: 10px;
  height: 90%;
  padding: 24px;
  margin-top: 24px;
  input {
    margin-bottom: 16px;
    width: 279px;
    height: 56px;
    background: #ffffff;
    border: 1px solid #dedede;
    border-radius: 5px;
    font-weight: 600;
    width: 90%;
    color: $Dark-Blue !important;
  }
  button {
    all: unset;
    background: #38cc8b;
    box-shadow: inset 0px -4px 0px rgba(0, 0, 0, 0.0908818);
    border-radius: 5px;
    width: 279px;
    height: 56px;
    cursor: pointer;
    margin-bottom: 8px;
    font-weight: 600;
    width: 90%;
    &:hover {
      background: $Green-Hover;
    }
  }
  p {
    color: $Grayish-Blue;
    font-size: 11px;
    margin-bottom: 10px;
  }
  span {
    color: $Red;
    font-weight: 700;
    font-size: 11px;
  }
}

@media (min-width: 1200px) {
  h1 {
    font-size: 50px;
  }
  .flex {
    display: flex;
    justify-content: space-evenly;
    background-image: url("../assets/bg-intro-desktop.png");
    .info-wrapper {
      width: 40%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      h1,
      p {
        text-align: left !important;
      }
    }
    .form-wrapper {
      width: 40%;
    }
  }
}
</style>
