<template>
  <div class="hello">
    <div v-if="createDom" class="container">
      <div v-for="(person, index) of people" v-bind:key="index" @click="redirect(person)" class="neon_card">
        <h1 class="title">{{ person.name }}</h1>
        <p class="planets">PLANET: {{homeWorlds[index].name}}</p>
      </div>
      <b-button-group class="buttons">
        <b-button @click="paginate(1, 10)" variant="outline-primary">1</b-button>
        <b-button @click="paginate(11, 21)" variant="outline-primary">2</b-button>
        <b-button @click="paginate(22, 31)" variant="outline-primary">3</b-button>
      </b-button-group>
    </div>
  <div class="img" v-else>
    <img src="../assets/spiner.gif" alt="">
  </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'HomePages',
  data: function() {
    return {
      people: [],
      homeWorlds: [],
      createDom: false
    }
  },
  async created() {
    for(let i=1; i<=10; i++){
      if(i!=17){
        await this.getPeople(i);
        await this.getHomeworld(i);
      }
    }
    this.createDom = true
  },
  methods: {
    async getPeople(i)  {
      try{
        let res = await axios.get(process.env.VUE_APP_BACK_ROUTE + `people/${i}`)
        this.people.push(res.data);
      }catch(err){
        console.log(err);
      }
    },
    async getHomeworld(i) {
      try{
        let res = await axios.get(process.env.VUE_APP_BACK_ROUTE + `planets/${i}`)
        this.homeWorlds.push(res.data);
      }catch(err){
        console.log(err);
      }
    },
    async paginate(start, end){
      this.createDom = false
      this.people = []
      this.homeWorlds = []
      for(start; start<=end; start++){
        if(start!=17){
          await this.getPeople(start);
          await this.getHomeworld(start);
        }
      }
      this.createDom = true
    },
    redirect(person){
      let urlArray = person.url.split("/")
      let id = urlArray[urlArray.length-2]
      this.$router.push({name:'Character', params:{id:id}})
    }
  }
}
</script>

<style lang="scss" scoped>
  @mixin displayCenter{
  /*  display: block; */
  /*     justify-content: center;
    align-items: center; */ 
  }

  .buttons{ 
    margin-left: 52%;
    margin-top: 110%;
  }

  .img{
    justify-content: center;
    align-items: center;
    display: flex;
    margin-left: 5%;
    margin-top: 15%;
  }

  .planets{
    text-align: center;
    font-size: 24px;
    color: #00daff;
  }

  .title{
    text-align: center;
    margin-block: 12%;
    font-size: 34px;
    color: #ffff;
  }

  .button{
    margin-left: 49%;
    margin-top: 109%;
  }

  .container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    width: 100%;
    height: 100%;

    .neon_card {
      width: 300px;
      height: 400px;
      background-image: url("../assets/fondo.jpg");
      margin: 10px;
      left: 30px;
      position: relative;
      @include displayCenter();

      &::before {
        position: absolute;
        content: '';
        background: linear-gradient(235deg, #89ff00, #060c21, #00bcd4);
        top: -2px;
        bottom: -2px;
        left: -2px;
        right: -2px;
        z-index: -1;
      }

      &::after {
        position: absolute;
        content: '';
        background: linear-gradient(235deg, #89ff00, #060c21, #00bcd4);
        top: -5px;
        bottom: -5px;
        left: -5px;
        right: -5px;
        z-index: -2;
        filter: blur(50px);
      }
    }
  }

@media (min-width: 962px) and (max-width: 1365px){

  .container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    width: 100%;
    height: 100%;

    .neon_card {
      width: 300px;
      height: 400px;
      background-image: url("../assets/fondo.jpg");
      margin: 10px;
      left: 30px;
      position: relative;
      @include displayCenter();

      &::before {
        position: absolute;
        content: '';
        background: linear-gradient(235deg, #89ff00, #060c21, #00bcd4);
        top: -2px;
        bottom: -2px;
        left: -2px;
        right: -2px;
        z-index: -1;
      }

      &::after {
        position: absolute;
        content: '';
        background: linear-gradient(235deg, #89ff00, #060c21, #00bcd4);
        top: -5px;
        bottom: -5px;
        left: -5px;
        right: -5px;
        z-index: -2;
        filter: blur(50px);
      }
    }
  }
  .buttons{
    margin-left: 80%;
    margin-top: 6%;
  }
}
@media (min-width: 361px) and (max-width: 960px){
  .buttons{
    right: 26%;
    margin-top: 3%;
  }

  .container {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    width: 100%;
    height: 100%;

    .neon_card {
      width: 300px;
      height: 400px;
      background-image: url("../assets/fondo.jpg");
      margin: 10px;
      left: 185px;
      position: relative;
      justify-content: center;
      align-items: center;

      &::before {
        position: absolute;
        content: '';
        background: linear-gradient(235deg, #89ff00, #060c21, #00bcd4);
        top: -2px;
        bottom: -2px;
        left: -2px;
        right: -2px;
        z-index: -1;
      }

      &::after {
        position: absolute;
        content: '';
        background: linear-gradient(235deg, #89ff00, #060c21, #00bcd4);
        top: -5px;
        bottom: -5px;
        left: -5px;
        right: -5px;
        z-index: -2;
        filter: blur(50px);
      }
    }
  }
}
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->

