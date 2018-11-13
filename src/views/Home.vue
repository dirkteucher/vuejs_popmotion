<template>
  <div class="home">
      <PopMotionSlider></PopMotionSlider>
  </div>
</template>

<script>
// @ is an alias to /src
import PopMotionSlider from '@/components/PopMotionSlider.vue'

export default {
  name: 'home',
  components: {
    PopMotionSlider
  }
}
</script>
