<template>
  <Header />
  <h1>Update Restaurant</h1>
  <form class="update">
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

    <button type="button" class="update-btn" v-on:click="updateRestaurant">
      Update Restaurant
    </button>
  </form>
</template>
<script>
import axios from 'axios'
import Header from './Header.vue';
export default {
  name: "Update",
  components:{
    Header
  },data(){
        return{
                restaurant:{
                    name:'',
                    address:'',
                    contact:''
                }

        }
  },methods:{
       async updateRestaurant(){
        let result = await axios.put("http://localhost:3000/restaurants/"+this.$route.params.id,{
            name:this.restaurant.name,
            address:this.restaurant.address,
            contact:this.restaurant.contact
        });

        if(result.status == 200){
                this.$router.push({name:"Home"});
        }
       }
  },
  async mounted() {
    //if user already exists we take him back to home page
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
     const result = await axios.get("http://localhost:3000/restaurants/"+this.$route.params.id);
   //console.warn(this.$route.params.id)
     console.warn(result);
     //to fill the forms with the data
     this.restaurant = result.data;
  },
};
</script>
