<template>
    <section>
        <div id="username">
            <img v-bind:src= rankimg>
            {{username}}
        </div>
        
        
        <table class="table">
            <tr>
                <th>Name</th>
                <td>{{name}}</td>
            </tr>
             <tr>
                <th>Platform</th>
                <td>{{platform}}</td>
            </tr>
            <tr>
                <th>Mobile</th>
                <td>{{number}}</td>
            </tr>
            <tr>
                <th>Email</th>
                <td>{{email}}</td>
            </tr>
        </table>

        <h2>Account Statistics</h2>
        
        <table class="table" id="table2">
            <tr>
                <th>kills</th>
                <td>{{stats}}</td>
            </tr>
            <tr>
                <th>Damage</th>
                <td>{{totaldmg}}</td>
            </tr>
            <tr>
                <th>Rank</th>
                <td>{{rank}}</td>
            </tr>
            <tr>
                <th>Selected Legend</th>
                <td>{{legendSelected}}</td>
            </tr>

            
        </table>
        <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>
        <Button type="button" id="stats" class="p-button-raised p-button-rounded p-button-md p-button-success" @click="fetchStats">Load Stats</Button>
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
                stats:{},
                totaldmg:{},
                rank:{},
                rankimg:{},
                legendSelected:{}

            }
        },

        

        methods:{
            back(){
                this.$router.back();
            },

            

            async fetchStats(){
                {
                    
                    fetch("https://apex-legends.p.rapidapi.com/stats/" +this.username+"/"+this.platform, {
                    "method": "GET",
                    "headers": {
                        "x-rapidapi-key": "2391a48f5cmsh3f13d8b9e281724p19e465jsn753ad679e2c1",
                        "x-rapidapi-host": "apex-legends.p.rapidapi.com"
                    }
                    })
                    .then(response => {
                    return response.json();
                    }).then(this.setResults)
                
                }
            },
            setResults:function(total){
                this.stats = total.total.kills.value;
                this.totaldmg = total.total.damage.value;
                this.rank = total.global.rank.rankName.toLowerCase() +" " + total.global.rank.rankScore;
                this.rankimg = total.global.rank.rankImg;
                this.legendSelected = total.legends.selected.LegendName.toUpperCase();
                console.log(this.stats);
            },

            async getData(){
            try{
                const response = await fetch("https://apexlegendsapp-cf377-default-rtdb.firebaseio.com/users/" + this.user1 + '.json',{
                    method:'GET'
                })
                const userData = await response.json();
                if(!response.ok){
                    console.log("something went wrong")
                }
                for (const id in userData){
                    this.name= userData[id].name.toUpperCase();
                    this.username=userData[id].username;
                    this.platform=userData[id].platform;
                    this.number= userData[id].number;
                    this.email= userData[id].email;
                }
               
            } catch(error){
                console.log(error);
            }
        },   
    },

    created(){
        this.user1 = this.$route.params.userID;
        
        this.getData();
    },

    mounted(){
        this.getData();
        this.fetchStats();
    },

    
}
</script>

<style scoped>

    #stats{
        margin-left: 10%;
    }    

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

    h2{
        position: absolute;
        top:60%;
        left:43%;
    }

    #username{
        font-size: 200%;
    }

    #stats{
        position: absolute;
        top:60%;
        left:25%;
    }
</style>