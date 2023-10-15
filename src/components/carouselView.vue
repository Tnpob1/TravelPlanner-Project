<template>
<carousel :per-page="1" :navigate-to="someLocalProperty" :mouse-drag="false">
    <slide>
      <div class="numbertext">ภูเก็ต</div>
          <img src="../assets/image/phuket2.jpg" style="width: 100%" />
    </slide>
    <slide>
      Slide 2 Content
    </slide>
  </carousel>

</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
export default {
  components: {
    Carousel,
    Slide
  }
};
</script>