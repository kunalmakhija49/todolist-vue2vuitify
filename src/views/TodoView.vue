<template>
<h3 v-if="user">Hi,{{user.name}}</h3>
<!--<h1>{{user}}</h1>-->
</template>

<script>
import axios from "axios";

export default {
  name:'HomeView',
  data(){
    return{
      user:null
    }
  },
  async created() {

      const response = await axios.get('http://127.0.0.1:8000/api/profile',{
        headers:{
          Authorization: 'Bearer '+localStorage.getItem('token')
        }

      });
    this.user = response.data;
      console.log(response);

  }
}
</script>