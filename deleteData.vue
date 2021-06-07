<template>
<transition name="slide-fade">
    <div class="modal-fade" id="deleteconfirmation" role="dialog">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h3 class="modal-title">Delete Member?</h3>
                </div>
                <div class="modal-body">
                    <p>Are you sure you want this deleted?</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-success" @click="getData()">Yes</button>
                    <button type="button" class="btn btn-danger" @click="returntolist()">No</button>
                </div>
            </div>
        </div>
    </div>
</transition>
</template>

<script>
export default{
    methods:{
        returntolist(){
            this.$router.push('/profiles');
        },

        

        async getData(){
            

            try{
                const response = await fetch("https://apexlegendsapp-cf377-default-rtdb.firebaseio.com/users/" + this.user1 +'.json',{
                    method:'DELETE'
                })

                if(!response.ok){
                    console.log("somehting went wrong");
                }

                this.$router.push('/fetching');

            } catch(error){
                console.log(error);
            }
        }

    },
    created(){
        this.user1 = this.$route.params.userID;
        
    }
    
}
</script>

<style scoped>

.slide-fade-leave-to{
        transform: translateY(-20px);
        opacity: 0;
    }

    .slide-fade-enter-from{
        opacity: 1;
        transform:translateY(20px)
    }

    .slide-fade-enter-active,
    .slide-fade-leave-active{
        transition: all 2s ease-out;
    }

</style>