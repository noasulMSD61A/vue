<template>
 <h2>{{username}}'s profile</h2>
    <section>
       
        <div id="username">
        </div>
        <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>
        <table class="table">
            <tr>
                <th>Name</th>
                <td>{{name}}</td>
            </tr>
            <tr>
                <th>Username</th>
                <td>{{username}}</td>
            </tr>
             <tr>
                <th>Platform</th>
                <td>{{platform}}</td>
            </tr>
            <tr>
                <th>Mobile</th>
                <td>{{phonecomp}}</td>
            </tr>
            <tr>
                <th>Email</th>
                <td>{{email}}</td>
            </tr>
            
        </table>
        
        <Button id="btn" @click="updateUser(res)" type="button" class="p-button-raised p-button-rounded p-button-lg p-button-success">Update</Button>
        
        <Button id="btn" @click="deleteUser(res)" type="button" class="p-button-raised p-button-rounded p-button-lg p-button-danger">Delete</Button>
        
    </section>
</template>

<script>
    export default{
        data(){
            return{
                user: '',
                name: '',
                username:'',
                platform:'',
                number: '',
                email:'',
                objectID: '',
            }
        },

        computed:{
            getUserUID(){
                return this.$store.getters.getCurrentUID
            },
            phonecomp() {
                return "+".concat(this.number);
            },
        },

        methods:{
            back(){
                this.$router.back();
            },

            updateUser(){
                
                this.$router.push('/update/' + this.getUserUID + '/' + this.objectID);
            },

            deleteUser(){
                
                this.$router.push('/delete/' + this.getUserUID);
            },

            async getData(){
            try{
                const response = await fetch("https://apexlegendsapp-cf377-default-rtdb.firebaseio.com/users/" + this.getUserUID +'.json',{
                    method:'GET'
                })
                const userData = await response.json();
                if(!response.ok){
                    console.log("something went wrong")
                }

                this.objectID = Object.keys(userData)[0];
                
                
                for (const id in userData){
                    this.name= userData[id].name.charAt(0);
                    this.username=userData[id].username;
                    this.platform=userData[id].platform;
                    this.number= userData[id].number;
                    this.email= userData[id].email;
                    //this.key=Object.keys(this.userData)[0];
                }
               
            } catch(error){
                console.log(error);
            }
        },   
    },
    mounted(){
        this.getData();
        
    },

    created(){
        this.user1 = this.$route.params.userID;
        
        this.getData();
    }
}
</script>

<style scoped>

    #back{
    position: absolute;
    left: 1%;
    top: 10%;
    }

    .table{
        width:30%;
        position: absolute;
        left:35%;
        border: 1px solid red;
        margin-top: 4%;
        box-shadow: 0px 0px 50px #cccccc;

    }

    #table2{
        position: absolute;
        top:60%;
    }

  

    #username{
        font-size: 200%;
    }

    #stats{
        position: absolute;
        top:60%;
        left:25%;
    }

    .fade-leave-to{
        transform: translateY(10px);
        opacity: 0;
    }

    .fade-enter-from{
        opacity: 1;
        transform:translateY(-10px)
    }

    .fade-enter-active,
    .fade-leave-active{
        transition: all 10s ease-out;
    }

    #btn{
        margin-top: 20%;
    }
</style>