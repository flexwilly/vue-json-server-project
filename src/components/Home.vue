<template>
  <Header />
  <h1>Hello {{ name }} , Welcome to Home page</h1>
  <table border="2px">
    <tr>
      <td>Id</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td colspan="2">Actions</td>
    </tr>
    <tr v-for="item in restaurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td><router-link :to="'/update/'+item.id">Update</router-link></td>
      <td><button v-on:click="deleteRestaurant(item.id)">Delete</button></td>
    </tr>
  </table>
</template>
<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
  name: "Home",
  components:{
    Header
  },
  data(){
      return{
        name:"",
        restaurant:[],
      }
   },
   methods:{
     async deleteRestaurant(id){
          let result = await axios.delete("http://localhost:3000/restaurants/"+id);
          console.warn(result)
          if(result.status == 200){
                    this.loadData();
          }
        },
          async loadData(){
            //if user already exists we take him back to home page
          let user = localStorage.getItem("user-info");
          this.name = JSON.parse(user).name;
          if (!user) {
            this.$router.push({ name: "SignUp" });
          }

          let result = await axios.get("http://localhost:3000/restaurants");
          console.warn(result);
          this.restaurant = result.data;
        },
    },

  async mounted() {
    this.loadData();
    }
  }
</script>
<style>
td{
  width:160px;
  height:40px;
}
</style>
