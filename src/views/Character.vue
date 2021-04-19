<template>
  <div class="hello">
    <section v-if="createDom" id="redirection" class="browser_alert">
      <div  id="main_content">
        <div class="title">
          <h2 class="Browser_title">{{selectedCharacter.data.name}}</h2>
        </div>
          <hr> 
          <h4>Vehicles:</h4>
          <h5 v-for="(vehicle,index) in vehicles" v-bind:key="index" class="">{{vehicle.name}}</h5>
          <hr>
          <h4>Films:</h4>
          <h5 v-for="(movie,index) in films" v-bind:key="'A' + index" class="">{{movie.title}}</h5>
          <hr>
          <h4>Starships:</h4>
          <h5 v-for="(starship,index) in starships" v-bind:key=" 'B' + index" class="">{{starship.name}}</h5>
      </div>
      <div id="background">
        <span></span>
      </div>
    </section>
    <div class="img" v-else>
      <img src="../assets/spiner.gif" alt="">
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'Character',

  data() {
    return{
      selectedCharacter: null,
      vehicles: [],
      films: [],
      starships: [],
      createDom: false
    }
  },

  async created() {
    let characterId = this.$route.params.id
    this.selectedCharacter = await axios.get(process.env.VUE_APP_BACK_ROUTE + `people/${characterId}/`)
    for(let i in this.selectedCharacter.data.vehicles){
      let vehicle = await axios.get(this.selectedCharacter.data.vehicles[i])
      this.vehicles.push(vehicle.data)
    }
    for(let i in this.selectedCharacter.data.films){
      let movie = await axios.get(this.selectedCharacter.data.films[i])
      this.films.push(movie.data)
    }
    for(let i in this.selectedCharacter.data.starships){
      let starship = await axios.get(this.selectedCharacter.data.starships[i])
      this.starships.push(starship.data)
    }
    this.createDom = true
  }
}
</script>

<style lang="scss" scoped>
.browser_alert {
  position: fixed;
  width: 100%;
  height: -webkit-fill-available;
  position: fixed;
  z-index: 3;
}
#background {
  background-image: url("../assets/fondo_2.jpg");
  width: 100%;
  position: fixed;
  height: 100%;
  opacity: 0.98;
  z-index: 1;
  box-shadow: 0 0 1rem 0 black;
  backdrop-filter: blur(6px);
}
#main_content {
    margin-top: 6px;
    left: 24%;
    top: 0%;
    position: fixed;
    z-index: 3;
    width: 57%;
    height: auto;
    background-color: #FFFFFF;
    border-radius: 10px;
    padding: 20px;
    overflow: auto;
}
.Browser_title {
  margin-left: 0;
  text-align: center;
}

  .img{
    justify-content: center;
    align-items: center;
    display: flex;
    margin-left: 5%;
    margin-top: 15%;
  }
</style>
