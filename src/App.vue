<template>
  <!---To show routes-->
  <router-view />
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

}
body{
  padding:0;
  margin:0;
}
.logo {
  width: 100px;
}
.register input,
.login input, .add input, .update input{
  width: 300px;
  height:40px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid purple;
}
.register-button,
.login-button, .add-btn, .update-btn {
  width: 320px;
  height: 40px;
  border: 1px solid purple;
  background: purple;
  color: white;
  cursor: pointer;
}
</style>
