<template>
    <form @submit.prevent="userRegistration">
        <Card>
        <template #title>
        <h2>Sign Up Form</h2>
        </template>
        
        <template #content>
        <div id="fgr" class="form-group row">
            <label :class="{error: $v.username.$error}" for="username" class="col-md-2 col-form-label"></label>
            <div class="col-sm-6">
                <div class="input-group">
                 <div class="input-group-prepend">
                 <span class="input-group-text"><i class="pi pi-id-card"></i></span>
                 </div>
                 <span class = "p-float-label">
                 <InputText :class="{error: $v.name.$error}" @blur="$v.name.$touch()" id="name" class="form-control p-inputtext-lg" type="text" v-model.trim="name"/>
                 <label :class="{error: $v.name.$error}" for="name">Name</label>
                 </span>
                </div>
            </div>
            <div v-if="$v.name.$error">
                    <div v-for="(error,index) of $v.name.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>
       

        <div id="fgr" class="form-group row">
            <label :class="{error: $v.username.$error}" for="username" class="col-md-2 col-form-label"></label>
            <div class="col-sm-6">
                <div class="input-group">
                 <div class="input-group-prepend">
                     <span class="input-group-text"><i class="pi pi-user"></i></span>
                 </div>
                 <span class = "p-float-label">
                 <InputText :class="{error: $v.username.$error}" @blur="$v.username.$touch()" id="username" class="form-control p-inputtext-lg" type="text" v-model.trim="username"/>
                 <label :class="{error: $v.username.$error}" for="username">Username</label>
                 </span>
                </div>
            </div>
            <div v-if="$v.username.$error">
                    <div v-for="(error,index) of $v.username.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div id="plt" class="form-group row">
            <label :class="{error: $v.platform.$error}" for="platform" class="col-md-2 col-form-label">platform</label>
            <div class="col-sm-3">
                <div class="input-group-prepend">
                     <span class="input-group-text"><i class="pi pi-sitemap"></i></span>
                      <select :class="{error: $v.platform.$error}" @blur="$v.platform.$touch()" id ="platform" name="platform" class="form-control" v-model.trim="platform">
                        <option value="PS4">PS4</option>
                        <option value="X1">XBOX</option>
                        <option value="PC">PC</option>
                      </select>
                 </div>
            </div>
            <div v-if="$v.platform.$error">
                    <div v-for="(error,index) of $v.platform.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>


        <div id="fgr" class="form-group row">
            <label :class="{error: $v.number.$error}" for="number" class="col-md-2 col-form-label"></label>
            <div class="col-sm-6">
                <div class="input-group mb-3">
                    <div class="input-group-prepend">
                        <select @blur="$v.countrycode.$touch()" id="countrycode" name="countrycode" class="form-control" v-model.trim="countrycode">
                            <option value="356">+356</option>
                            <option value="0044">+0044</option>
                        </select>
                    </div>
                    <span class = "p-float-label">
                    <InputText :class="{error: $v.number.$error}" @blur="$v.number.$touch()" id="number" class="form-control" type="text" v-model.number="number"/>
                    <label :class="{error: $v.number.$error}" for="number">Phone</label>
                    </span>
                </div>
            </div>
            <div v-if="$v.number.$error">
                    <div v-for="(error,index) of $v.number.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div  id="fgr" class="form-group row">
            <label :class="{error: $v.email.$error}" for="email"  class="col-md-2 col-form-label"></label>
            <div class="col-sm-6">
                <div class="input-group">
                 <div class="input-group-prepend">
                     <span class="input-group-text"><i class="pi pi-send"></i></span>
                 </div>
                 <span class = "p-float-label">
                 <InputText :class="{error: $v.email.$error}" @blur="$v.email.$touch()"  id="email" class="form-control p-inputtext-lg" type="email" v-model.trim="email"/>
                 <label :class="{error: $v.email.$error}" for="email">Email</label>
                 </span>
                </div>
            </div>
            <div v-if="$v.email.$error">
                    <div v-for="(error,index) of $v.email.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div id="fgr" class="form-group row">
            <label :class="{error: $v.password.$error}" for="password" class="col-md-2 col-form-label"></label>
            <div class="col-sm-6">
                <div class="input-group">
                 <div class="input-group-prepend">
                     <span class="input-group-text"><i class="pi pi-lock"></i></span>
                 </div>
                 <span class = "p-float-label">
                 <InputText :class="{error: $v.password.$error}" @blur="$v.password.$touch()" id="password" class="form-control p-inputtext-lg" type="password" v-model.trim="password"/>
                 <label :class="{error: $v.password.$error}" for="password">Password</label>
                 </span>
                </div>
            </div>
            <div v-if="$v.password.$error">
                    <div v-for="(error,index) of $v.password.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div id="fgr" class="form-group row">
            <label :class="{error: $v.Cpassword.$error}" for="Cpassword" class="col-md-2 col-form-label"></label>
            <div class="col-sm-6">
                <div class="input-group">
                 <div class="input-group-prepend">
                     <span class="input-group-text"><i class="pi pi-lock"></i></span>
                 </div>
                 <span class = "p-float-label">
                 <InputText :class="{error: $v.Cpassword.$error}" @blur="$v.Cpassword.$touch()" id="Cpassword" class="form-control p-inputtext-lg" type="password" v-model.trim="Cpassword"/>
                 <label :class="{error: $v.Cpassword.$error}" for="Cpassword">Confirm Password</label>
                 </span>
                </div>
            </div>
            <div v-if="$v.Cpassword.$error">
                    <div v-for="(error,index) of $v.Cpassword.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>

        <div id="fgr" class="form-group row">
            <label for="terms" class="col-md-2 col-form-label">Terms and Conditions</label>
            <div class="form-check">
                <input type="checkbox"  class="form-check-input" id="TCcheck" v-model.trim="TCcheck">
                <label id ="TAC" class="form-check-label" for="TCcheck">I have read and understood the terms and Conditions</label>
            </div>
            <div v-if="$v.TCcheck.$error">
                    <div v-for="(error,index) of $v.TCcheck.$errors" :key="index">
                        <div class="text-danger">{{error.$message}}</div>
                    </div>
                </div>
        </div>
        </template>
        
        
        <template #footer>
        <Button id="submit" type="submit" :disabled="$v.$invalid || !TCcheck" label="Submit" class="p-button-raised p-button-rounded p-button-lg p-button-success" ></Button>
        <Button id="login" @click="toSignIn" label="Log in" class="p-button-raised p-button-rounded p-button-lg " ></Button>
        </template>
        </Card>

    </form>
    <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>
</template>

<script>
import {required, alpha, numeric, minLength, maxLength, email, sameAs} from '@vuelidate/validators'
import firebase from 'firebase'

export default {
    data(){
        return{
            platforms:[
                {name:'PS4'},
                {name:'X1'},
                {name:'PC'},

            ],

            countrycodes:[
                {name:'356'},
                {name:'0044'}
            ],

            show: true,
            user: {
                cname:'',
                

            },

            name: '',
            username:'',
            platform:'',
            countrycode:'',
            number: '',
            email:'',
            password:'',
            Cpassword:'',
            TCcheck:''
        };
    },
    validations(){
        return{
            name:{required, alpha},
            username:{required},
            platform:{required},
            number: {required, numeric, minLength:minLength(8),maxLength:maxLength(8)},
            email:{required, email},
            password:{required, minLength:minLength(3)},
            Cpassword:{required, cpass: sameAs(this.password)},
            TCcheck:{required}
        }
    },
    methods: {
        toSignIn(){
                this.$router.push('/login');
        },

        back(){
            this.$router.back();
        },

        userRegistration() {
            this.user.cname = this.name

            firebase
            .auth()
            .createUserWithEmailAndPassword(this.email, this.password)
            .then((res) => {
                res.user
                .updateProfile({
                    displayName: this.user.cname
                })
                .then(() => {
                    this.$router.push('/login')
                    this.submitForm(res.user.uid);
                });
            })
            .catch((error) => {
                alert(error.message);
            });
        },
        

        async submitForm(useruid){
            this.$v.$touch();

            if (!this.$v.$invalid){
                
                const response = await fetch("https://apexlegendsapp-cf377-default-rtdb.firebaseio.com/users/" + useruid + ".json", {
                    method: 'POST',
                    headers: {
                        'Content-Type':'application/json'
                    },
                    body: JSON.stringify({
                        name:this.name,
                        username:this.username,
                        platform:this.platform,
                        number:this.countrycode + "" + this.number,
                        email:this.email,
                        password:this.password
                    })
                    
                })
                if(!response.ok){
                    console.log("something crashed");
                }
                this.$router.push("/login")
            }
        },
    },
};


</script>

<style scoped>

#back{
    position: absolute;
    left: 1%;
    top: 10%;
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
    
    padding-bottom: 3%;
    
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

.slide-up-enter-from{
    transform: translateY(10px);
    opacity: 0;
}

.slide-up-enter-active{
    transform: translateY(10px);
    opacity: 0;
}

#submit{
    position: absolute;
    top:85%;
    left:40%;
}

#login{
    position: absolute;
    top:85%;
    right:70%;
}

.p-card{
    width: 40%;
    margin-left: 27%;
    margin-top:5%;
    box-shadow: 0px 0px 100px #cccccc;
}

.input-group{
    padding:5px;
    margin-left: 20%;
}

#plt{
    padding:5px;
    margin-left: 10%;
}


</style>