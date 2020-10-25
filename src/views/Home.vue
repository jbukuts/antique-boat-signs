<template>
  <div class="home">
    <!--<carousel :perPage=1 :loop=true :autoplay=true :autoplayTimeout=5000 :paginationEnabled='false'>
      <slide  v-for="(image,i) in this.images" :key="i">
        <img :src="image.src" style="width: 60%"/>
      </slide>
    </carousel>-->

    <Carousel></Carousel>

    <div id="desc">
      More Signs
    </div>

  </div>
</template>

<script>
// @ is an alias to /src
//import { Carousel, Slide } from 'vue-carousel';
import Carousel from '../components/Carousel.vue';

export default {
  name: 'Home',
  components: {
    Carousel
    //Carousel,
    //Slide,
  },
  data() {
    return {}
  },
  mounted() {
  
  }
}
</script>

<style scoped>

.home {
  width: 100%;
  color: white;
}

#desc {
  width: 100%;
  height: 100%;
  background: rgb(131, 131, 131);
}



</style>
