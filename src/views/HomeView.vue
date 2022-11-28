<template>
  <div class="home">
    <HeaderComponent />
    <SliderComponent />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderComponent from '@/components/HeaderComponent.vue';
import SliderComponent from '@/components/SliderComponent.vue';


export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
    SliderComponent
  }
}
</script>

