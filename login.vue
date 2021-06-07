<template>
    <div class="vue-tempalte">
        <form @submit.prevent="userLogin">
          <Card>
            <template #header>
              <img src="../assets/apexbackground.jpg">
            </template>

            <template #title>
              <h3>Sign In</h3>
            </template>

            <template #content>
            <div class="form-group">
              <span class = "p-float-label">
                <InputText id="email" type="email" class="form-control form-control-lg p-inputtext-lg" v-model="user.email" />
                <label for="email">Email Address</label>
              </span>
            </div>

            <div class="form-group">
                <span class = "p-float-label">
                <InputText id="password" type="password" class="form-control form-control-lg" v-model="user.password" />
                <label for="password">Password</label>
                </span>
            </div>
            </template>

            <template #footer>
              <Button label="Log In" type="submit" class="p-button-raised p-button-rounded p-button-lg p-button-secondary"></Button>
            </template>
            <p class="forgot-password text-right mt-2 mb-4">
                <router-link to="/forgot-password">Forgot password ?</router-link>
            </p>
            
          </Card>
        </form>
        <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>
    </div>
</template>


<script>
import firebase from "firebase";

export default {
  data() {
    return {
      user: {   
        email: '',
        password: ''
      }
    };
  },
  methods: {
    back(){
        this.$router.back();
    },
    userLogin() {
        firebase
        .auth()
        .signInWithEmailAndPassword(this.user.email, this.user.password)
        .then((res) => {
            this.$store.dispatch('setCurrentUID', res.user.uid)
            this.$store.dispatch('setAuth',true);
            console.log("logged in")
        })
        .catch((error) => {
          alert(error.message);
        });
        this.$router.push('/fetching');
    }
  }

};
</script>

<style scoped>

#back{
    position: absolute;
    left: 1%;
    top: 10%;
}


form{
  width:50%;
  margin: auto;
}

.p-card{
  width:60%;
  margin-left: 25%;
  margin-top:3%;
  box-shadow: 0px 0px 100px #cccccc;
}

.form-group{
    padding:5px;
}





</style>