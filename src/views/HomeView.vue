<template>

  <!--  <hello-world />-->
  <!-- <v-app>-->
  <!--   <v-card row wrap class="my-3">-->
  <!--   <v-form>-->
  <!--     <v-flex xs5 md3>-->
  <!--     <v-text-field  label="Name" type="text" required></v-text-field>-->
  <!--     </v-flex>-->
  <!--     <v-flex md3>-->
  <!--     <v-text-field  label="abc" type="text"></v-text-field>-->
  <!--     </v-flex>-->
  <!--     <v-flex md3>-->
  <!--     <v-text-field  label="abc" type="text"></v-text-field>-->
  <!--     </v-flex>-->
  <!--     <v-flex md3>-->
  <!--     <v-text-field  label="abc" type="text"></v-text-field>-->
  <!--     </v-flex>-->
  <!--   </v-form>-->
  <!--   </v-card>-->
  <!-- </v-app>-->
  <v-app>
    <v-main>


      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <h1 class="text-center">login</h1>
            <v-card class="elevation-12">

              <v-window v-model="step">

                <v-window-item :value="1">

                  <v-row>

                    <v-col cols="12" md="12">
                      <v-form @submit.prevent="loginform">
                      <v-card-text class="m12">

                          <!--                    <h1 class="text-center display-2 teal&#45;&#45;text text&#45;&#45;accent-3">Sign In</h1>-->
                          <v-text-field label="Email" type="text" required v-model="email"></v-text-field>
                          <!--                    <div class="text-center" ></div>-->
                      </v-card-text>
                      <v-card-text class="m12">
                        <!--                    <h1 class="text-center display-2 teal&#45;&#45;text text&#45;&#45;accent-3">Sign In</h1>-->
                        <v-text-field label="Password" type="password" required v-model="password"></v-text-field>
                        <!--                      <div class="text-center" ></div>-->
                      </v-card-text>
                      <v-col class="d-flex" cols="12" sm="3" xsm="12">
                        <v-btn color="success" class="mr-4" type="submit"> Login</v-btn>


                        <!--                      <v-btn color="primary" class="mr-5">signup</v-btn>-->
                      </v-col>

                      </v-form>

                    </v-col>
                    <v-col cols="12" md="4">
                      <!--                  <h1>hello</h1>-->
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>

</template>

<script>
// import HelloWorld from '../components/HelloWorld'
import axios from "axios";
export default {

  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Home',

  components: {
    // HelloWorld,
  },
  data: () => {
    return {
      // errors: [],
      email: '',
      password: '',
      step: 1,
    }

  },
  props: {
    source: String,
  },
  methods: {
    checkForm(){
      if(this.email && this.password){
        return true;
      }
      // this.errors = [];

      if(!this.email){
        this.errors.push('Please enter Email');
      }
      if(!this.password){
        this.errors.push('Enter Password');
      }

      console.log('submitted');

    },
     loginform(){
    // var response = await axios.post('http://127.0.0.1:8000/api/login',{
    //   email:this.email,
    //   password:this.password
    //
    // });
       let axiosConfig = {
         headers: {
           'Content-Type': 'application/json;charset=UTF-8',
           "Access-Control-Allow-Origin": "*",
         }
       };
       axios.post('http://127.0.0.1:8000/api/login',{
         email:this.email,
         password:this.password
       },axiosConfig
       ).then((response)=>{
         if(response.data.status == 1){
           this.$router.push({name:"TodoView"});
         }
         console.log(response.data.token.original.access_token);
         localStorage.setItem('token',response.data.token.original.access_token);
       })



    // console.log("this is response which we get"+response);

    }

  }
}

</script>
