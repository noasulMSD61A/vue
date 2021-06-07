<template>
    <h2>Update Your Information</h2>
    <form @submit.prevent="submitForm">
        <div class="form-group row">
            <label :class="{error: $v.name.$error}" for="name" class="col-md-2 col-form-label">Name</label>
            <div class="col-sm-6">
                <input :class="{error: $v.name.$error}" @blur="$v.name.$touch()" id="name" class="form-control" type="text" v-model.trim="name"/>
            </div>
            <div v-if="$v.name.$error">
                    <div v-for="(error,index) of $v.name.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div class="form-group row">
            <label :class="{error: $v.username.$error}" for="username" class="col-md-2 col-form-label">Username</label>
            <div class="col-sm-6">
                <div class="input-group">
                 <div class="input-group-prepend">
                     <span class="input-group-text"><i class="fa fa-user-circle"></i></span>
                 </div>
                 <input :class="{error: $v.username.$error}" @blur="$v.username.$touch()" id="username" class="form-control" type="text" v-model.trim="username"/>
                </div>
            </div>
            <div v-if="$v.username.$error">
                    <div v-for="(error,index) of $v.username.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div class="form-group row">
            <label :class="{error: $v.platform.$error}" for="platform" class="col-md-2 col-form-label">Platform</label>
            <div class="col-sm-6">
                <select :class="{error: $v.platform.$error}" @blur="$v.platform.$touch()" id ="platform" name="platform" class="form-control" v-model.trim="platform">
                    <option value="PS4">PS4</option>
                    <option value="X1">XBOX</option>
                    <option value="PC">PC</option>
                </select>
            </div>
            <div v-if="$v.platform.$error">
                    <div v-for="(error,index) of $v.platform.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div class="form-group row">
            <label :class="{error: $v.email.$error}" for="email"  class="col-md-2 col-form-label">Email</label>
            <div class="col-sm-6">
                <input :class="{error: $v.email.$error}" @blur="$v.email.$touch()" id="email" class="form-control" type="email" v-model.trim="email"/>
            </div>
            <div v-if="$v.email.$error">
                    <div v-for="(error,index) of $v.email.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div class="form-group row">
            <label :class="{error: $v.number.$error}" for="number" class="col-md-2 col-form-label">Phone Number</label>
            <div class="col-sm-6">
                <div class="input-group mb-3">
                    <div class="input-group-prepend">
                        <select  id="countcodes" name="countrycodes" class="form-control">
                            <option value="Malta">+356</option>
                            <option value="England">+0044</option>
                        </select>
                    </div>
                    <input :class="{error: $v.number.$error}" @blur="$v.number.$touch()" id="number" class="form-control" type="text" v-model.number="number"/>
                </div>
            </div>
            <div v-if="$v.number.$error">
                    <div v-for="(error,index) of $v.number.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <Button class="p-button-raised p-button-rounded p-button-lg p-button-primary" type="submit" :disabled="$v.$invalid" >Submit</Button>
        <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>


    </form>
</template>

<script>
import {alpha, numeric, minLength, maxLength, email} from '@vuelidate/validators'

export default {
    data(){
        return{
            name: '',
            username: '',
            platform: '',
            number: '',
            email:'',
        };
    },
    validations(){
        return{
            name:{alpha},
            username:{},
            platform:{},
            number: {numeric, minLength:minLength(8),maxLength:maxLength(8)},
            email:{email},
        }
    },

    computed:{
            getUserUID(){
                return this.$store.getters.getCurrentUID
            }
        },
    
    methods: {
        back(){
            this.$router.back();
        },

        async submitForm(){
            this.$v.$touch();

            if (!this.$v.$invalid){
                const response = await fetch("https://apexlegendsapp-cf377-default-rtdb.firebaseio.com/users/" + this.user1+ '/'+ this.objID+  '.json', {
                    method: 'PUT',
                    headers: {
                        'Content-Type':'application/json'
                    },
                    
                    body: JSON.stringify({
                        
                        name:this.name,
                        username:this.username,
                        platform:this.platform,
                        number:this.number,
                        email:this.email,
                        
                    })
                })
                console.log();
                if(!response.ok){
                    console.log("something crashed");
                }
                this.$router.push("/fetching")
            }
        },
  
    },
    created(){
        this.user1 = this.$route.params.userID;
        this.objID = this.$route.params.objectID;
        console.log(this.user1)
        console.log(this.objID)
    },

    
}

</script>

<style scoped>

#back{
    position: absolute;
    left: 1%;
    top: 10%;
}

form{
    display: inline-block;
    width: 70%;
    margin-left: 15%;
    margin-top: 5%;
}

label{
    text-align: right;
}

button{
    margin-right: -23%;
}

#TAC{
    color:blue;
}

#TCcheck{
    margin-left:100%;
}

h2{
    
    margin-top: 3%;;
    
}

text-danger{
    text-align: left;
}

.text-danger:active{
    border-color: red;
}

label.error{
    color:red;
}

input.error, select.error{
    border: 2px solid red;
}


</style>