<template>
  <div>
    <img class="logo" src="../assets/itnlogo.jpg" />
    <h1>Login</h1>
    <div class="login">
      <br /><br />
      <input type="email" placeholder="Enter Email" v-model="email" />

      <input type="password" placeholder="Enter Password" v-model="password" />

      <button v-on:click="login" class="login-button">Login</button>
      <p>
        <router-link to="/signUp">SignUp</router-link>
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      //console.warn(result);
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    //if user already logged in  we take him back to home page
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
