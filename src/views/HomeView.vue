<template>
  <div class="home">
    <HeaderComponent />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderComponent from '@/components/HeaderComponent.vue';

export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
  }
}
</script>
