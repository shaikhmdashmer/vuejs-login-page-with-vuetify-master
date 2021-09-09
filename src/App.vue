<template>
<div>
  <v-app>
    <div class="backgruond"></div>
    <v-main class="d-flex justify-center align-center">
      <v-col cols="10" lg="4" class="mx-auto">
        <v-card class="pa-4">
          <div class="text-center">
            <v-avatar size="100" color="indigo lighten-4">
              <v-icon size="40" color="indigo">mdi-account</v-icon>
            </v-avatar>
            <h2 class="indigo--text">Vue login Page</h2>
          </div>
          <v-form @submit.prevent="submitHandler" ref="form">
            <v-card-text>
              <v-text-field
                v-model="email"
                :rules="emailRules"
                type="email"
                label="Email"
                placeholder="Email"
                prepend-inner-icon="mdi-account"
                required
              />
              <v-text-field
                      v-model="password"
                      :rules="passwordRules"
                      :type="passwordShow?'text':'password'"
                      label="Password"
                      placeholder="Password"
                      prepend-inner-icon="mdi-key"
                      :append-icon="passwordShow ? 'mdi-eye':'mdi-eye-off'"
                      @click:append="passwordShow = !passwordShow"
                      required
              />
              <v-switch label="Remember me" color="indigo"></v-switch>
            </v-card-text>
            <v-card-actions class="justify-center">
              <button :loading="loading" type="submit" class="home1" @click="goToHome()">
                <span class="white--text px-8">Login</span>
              </button>
              
            </v-card-actions>
          </v-form>
        </v-card>
      </v-col>
    </v-main>
    <v-snackbar top color="green" v-model="snackbar">
      Login success
    </v-snackbar>
  </v-app>
  <div id="load1">
    <my-app/>
  </div>
  </div>
</template>

<script>
import MyApp from './MyApp.vue';

export default {
  components: { MyApp },
  name: 'App',


  data: () => ({
    loading:false,
    snackbar:false,
    passwordShow:false,
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    password: '',
    passwordRules: [
      v => !!v || 'Password is required',
      v => (v && v.length >= 6) || 'Password must be 6  characters or more!',
    ],
  }),
  methods:{
    submitHandler(){
      if (this.$refs.form.validate()){
          this.loading = true
          document.getElementById("load1").style.display="block"
        setTimeout(()=> {
          this.loading = false
          this.snackbar = true
        },3000)
      }
    }
  },
   goToHome(){
  //  this.$router.push('/my-app'); 
  //     }
  this.$router.push({name:'my-app', params: {id: '[load1]'}});} 
};
</script>
<style>
  .backgruond{
    background-image: url(https://images.unsplash.com/photo-1581697723996-75f12879cabb?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80) !important;
    height: 300px;
    width: 100%;
    display: block;
    position: absolute;
    top: 0;
    background-size: cover;
  }
  #load1{
    display: none;
  }
  .home1{
    background-color: #3f51b5;
    padding: 5px 10px;
    border-radius: 5px;
  }

</style>