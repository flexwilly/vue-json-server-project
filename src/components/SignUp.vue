<template>
  <div>
    <img class="logo" src="../assets/itnlogo.jpg" />
    <h1>Sign Up</h1>
    <div class="register">
      <br /><br />
      <input type="text" placeholder="Enter Name" v-model="name" />
      <input type="email" placeholder="Enter Email" v-model="email" />
      <input type="password" placeholder="Enter Password" v-model="password" />

      <button v-on:click="signUp" class="register-button">Sign Up</button>
      <p>
        <router-link to="/login">Login</router-link>
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/users", {
        email: this.email,
        name: this.name,
        password: this.password,
      });

      console.warn(result);
      if (result.status == 201) {
        //alert("sign up done");
        //redirect user to home after sign up
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    //if user already exists we take him back to home page
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
<style></style>
