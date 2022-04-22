<template>
  <v-app>
    <v-main>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <h1 class="text-center">Signup</h1>
            <v-card class="elevation-12">

              <v-window v-model="step">

                <v-window-item :value="1">

                  <v-row>
                    <v-col cols="12" md="12">
                      <v-form @submit.prevent='handlesubmit'>

                        <v-card-text class="m12">
                          <!--                    <h1 class="text-center display-2 teal&#45;&#45;text text&#45;&#45;accent-3">Sign In</h1>-->
                          <v-text-field label="name" type="text" required v-model="name"></v-text-field>
                          <!--                    <div class="text-center" ></div>-->
                        </v-card-text>
                        <v-card-text class="m12">
                          <!--                    <h1 class="text-center display-2 teal&#45;&#45;text text&#45;&#45;accent-3">Sign In</h1>-->
                          <v-text-field label="Email" type="email" required v-model="email"></v-text-field>
                          <!--                      <div class="text-center" ></div>-->
                        </v-card-text>
                        <v-card-text class="m12">
                          <!--                    <h1 class="text-center display-2 teal&#45;&#45;text text&#45;&#45;accent-3">Sign In</h1>-->
                          <v-text-field label="password" type="password" required v-model="password"></v-text-field>
                          <!--                    <div class="text-center" ></div>-->
                        </v-card-text>
                        <v-card-text class="m12">
                          <!--                    <h1 class="text-center display-2 teal&#45;&#45;text text&#45;&#45;accent-3">Sign In</h1>-->
                          <v-text-field label="Confirm Password" type="password" required v-model="confirm_password"></v-text-field>
                          <!--                    <div class="text-center" ></div>-->
                        </v-card-text>
                        <v-col class="d-flex" cols="12" sm="3" xsm="12">
                          <!--                        <v-btn  color="success" class="mr-4"> Login </v-btn>-->
                          <v-btn color="primary" class="mr-5" type="submit">Register</v-btn>
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
import axios from 'axios'
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Home',

  components: {
    // HelloWorld,
  },
  data: () => {
    return {
      name: '',
      email:'',
      password:'',
      confirm_password: '',


      step: 1,
    }

  },
  props: {
    source: String,
  },
  methods: {
    handlesubmit(){
      const  form_data = {
        name: this.name,
        email :this.email,
        password:this.password,
        // confirm_password: this.confirm_password,

      };
      console.log(form_data);
      axios.post('http://127.0.0.1:8000/api/register',form_data).
      then(response=>{
        console.log(response)
        console.log('record inserted')
        this.$router.push('/')
      }).catch(
          error=>{
            console.log(error)
          }
      )
    }
  }
}

</script>

