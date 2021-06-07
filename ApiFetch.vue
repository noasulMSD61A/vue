<template >
<h5 style="margin-top: 10px;">APEX LEGENDS NEWS</h5>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
<div class="container">
  <div class="row mb-5">
    <select type = "text" placeholder="Enter Gamertag" v-model="query" class="form-control" @keypress="fetchNews" >
                    <option value="en-gb">English(gb)</option>
                    <option value="en-us">English(us)</option>
                    <option value="fr">French</option>
                    <option value="de">German</option>
    </select>
  </div>
    <div class ="row">
      <div v-for="(row) in title" :key="row.id">-->
        <div class="card ml-3" style="width: 22rem; height:30rem;">
          <img class="card-img-top" v-bind:src=row.img alt="Card image cap">
          <div class="card-body">
            <h5 class="card-title">{{row.title}}</h5>
            <p class="card-text">{{row.short_desc}}</p>
            <a target="_blank" v-bind:href=row.link class="btn btn-primary" style="position: absolute; top: 90%; left:38%;">See Full</a>
          </div>
        </div>
      </div>
    </div>
  </div>
  <Button type="button" id="back" class="p-button-raised p-button-rounded p-button-lg p-button-help" @click="back">Back</Button>
</template>

<script>
export default {
  name: 'App.vue',
  data(){
    return{
      query:'',
      title:{}
    }
  },
  methods:{
    back(){
        this.$router.back();
    },

    fetchNews(e){
      if(e.key == 'Enter'){
        fetch("https://apex-legends.p.rapidapi.com/news/" +this.query, {
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
    setResults:function(results){
      this.title = results;
      console.log(this.title);
    }
  }
}
</script>

<style scoped>
  #back{
    position: absolute;
    left: 1%;
    top: 10%;
}
</style>
