<template>
  <div class="hello">
    <div v-if="createDom" class="container">
      <div v-for="(person, index) of people" v-bind:key="person.id"  class="neon_card">
          <!-- <img src="../assets/fondo.jpg" alt=""> -->
          <h1 class="title">{{ person.name }}</h1>
          <p>{{homeWorlds[index].name}}</p>
      </div>
      <div class="pagination">
        <b-pagination-nav pills  number-of-pages="10" base-url="#"></b-pagination-nav>
      </div>
    </div>
    <div class="img" v-else>
      <img src="../assets/spiner.gif" alt="">
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'HelloWorld',
  data: function() {
    return {
      people: [],
      homeWorlds: [],
      pages: 1,
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
    }
  }
}
</script>

<style lang="scss" scoped>
  @mixin displayCenter{
/*     display: block;
/*     justify-content: center;
    align-items: center; */ 
  }

  .img{
    justify-content: center;
    align-items: center;
    display: flex;
    margin-left: 5%;
    margin-top: 22%;
  }

  .title{
    text-align: center;
    margin-block: 12%;
  }

  .hello{
    width: 100%;
    min-height: 100vh;
    background: #0000;
    color: #ffff;
    // @include displayCenter();
  }

  .pagination{
    margin-top: 131%;
    margin-left: 25%;
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
            // @include displayCenter();

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
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->

