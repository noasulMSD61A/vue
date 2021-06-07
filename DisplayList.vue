<template >

    <div class="container">
        <section v-if="!results.length">
            No Members Yet
        </section>

        <section v-else>
            <div class="table-responsive">
                <table class="table">
                    
                        <thead>
                            <tr>
                                <th  scope="col">View</th>
                                <th  scope="col">Name</th>
                                <th  scope="col">Email</th>

                            </tr>
                        </thead>
                    
                
                        <tbody name="tr" itemscope="transition-group">
                            
                                <tr v-for="res in results" :key="res.id" >
                                    <td><button @click="viewInfo(res)" type="button" class="btn btn-info">View</button></td>
                                    <td>{{res.username}}</td>
                                    <td>{{res.email}}</td>
                                </tr>
                            
                        </tbody>
                </table> 
            </div>
        </section>
   </div>
     <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>

</template>

<script>
    export default{
        data(){
            return{
                results:[],
                nodes: null
                
                
                
            };
        },

        computed:{
            getUserUID(){
                return this.$store.getters.getCurrentUID
            }
        },

        methods:{
            back(){
                this.$router.back();
            },

            viewInfo(user){
                const userID = user.id;
                console.log("user id: " + userID)
                this.$router.push('/view/' + userID);
            },

            updateUser(user){
                const userID = user.id;
                this.$router.push('/update/' + userID);
            },

            deleteUser(user){
                const userID = user.id;
                this.$router.push('/delete/' + userID);
            },

            async getData(){
            try{
                const response = await fetch("https://apexlegendsapp-cf377-default-rtdb.firebaseio.com/users.json",{
                    method:'GET'
                })
                const responseData = await response.json();
                if(!response.ok){
                    console.log("something went wrong")
                }
                console.log(responseData)
                const results = [];
                
                for (const id in responseData){
                   const temp = responseData[id]
                   const obj = Object.values(temp)
                   console.log(obj)
                    results.push({
                        id:id,
                        username: obj[0].username.toUpperCase(),
                        email: obj[0].email,
                       
                    });
                    this.results = results;
                    console.log(results)
                }
                
            } catch(error){
                console.log(error);
            }
        },   
    },
   
    mounted(){
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

    .container{
        max-width: 50%;
        margin-left: 25%;
        margin-top:2%;
        padding:0px;
    }
    
    .slide-right-enter-from{
        transform: scale(0.6);
        opacity: 0;
    }

    .slide-right-enter-to{
        transform: scale(1);
        opacity: 1;
    }


    .slide-right-enter-active{
        transition: all 2s ease;
    
    }
    
    

</style>
