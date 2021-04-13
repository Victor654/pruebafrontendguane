<template>
  <div class="hello">
    <div class="container">
      <div class="neon_card">
        <h1>Hello</h1>
      </div>
      <div class="neon_card second">
        <h1>Every one</h1>
      </div>
      <div class="neon_card third">
        <h1>welcome</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
}
</script>

<style lang="scss" scoped>
  @mixin displayCenter{
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .hello{
    width: 100%;
    min-height: 100vh;
    background: #0000;
    color: #ffff;
    @include displayCenter();
  }
  
.container {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        width: 100%;
        height: 100%;

        .neon_card {
            width: 300px;
            height: 400px;
            background: #000000;
            margin: auto;
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

        .second {
            &::before {
                background: linear-gradient(235deg, #ffbb00, #060c21, #d40063);

            }

            &::after {
                background: linear-gradient(235deg, #ffbb00, #060c21, #d40063);

            }

        }

        .third {
            &::before {
                background: linear-gradient(235deg, #e100ff, #060c21, #3700ff);

            }

            &::after {
                background: linear-gradient(235deg, #e100ff, #060c21, #3700ff);

            }

        }
    }
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->

