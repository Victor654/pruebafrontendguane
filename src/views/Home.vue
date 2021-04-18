<template>
  <div class="home">
    <HomePages/>
  </div>
</template>

<script>
// @ is an alias to /src
import HomePages from '@/components/HomePages.vue'

export default {
  name: 'Home',
  components: {
    HomePages
  },
}
</script>

