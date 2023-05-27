<template>
  <Header />
  <h1>Add Restaurant</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      v-model="restaurant.name"
      placeholder="Enter Name"
    />
    <input
      type="text"
      name="address"
      v-model="restaurant.address"
      placeholder="Enter Address"
    />

    <input
      type="text"
      name="contact"
      v-model="restaurant.contact"
      placeholder="Enter Contact"
    />

    <button type="button" class="add-btn" v-on:click="addRestaurant">
      Add Restaurant
    </button>
  </form>
</template>
<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
  name: "Add",
  components:{
    Header
  },
  data(){
        return{
                restaurant:{
                    name:'',
                    address:'',
                    contact:''
                }

        }
  },methods:{
      async addRestaurant(){
          //console.warn(this.restaurant);
          const result = await axios.post("http://localhost:3000/restaurants",{
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact
          });
          if(result.status == 201){
                this.$router.push({name:"Home"});
          }
          console.log("result:",result);
      }
  },
  mounted() {
    //if user already exists we take him back to home page
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
