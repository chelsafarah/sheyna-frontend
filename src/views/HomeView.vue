<template>
  <div class="home">
    <HeaderComponent />
    <SliderComponent />
    <ProductSlider />
    <InstaGallery /> 
    <PartnerLogo /> 
    <FooterComponent /> 
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderComponent from '@/components/HeaderComponent.vue';
import SliderComponent from '@/components/SliderComponent.vue';
import ProductSlider from '@/components/ProductSlider.vue';
import InstaGallery from '@/components/InstaGallery.vue';
import PartnerLogo from '@/components/PartnerLogo.vue';
import FooterComponent from '@/components/FooterComponent.vue';


export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
    SliderComponent,
    ProductSlider,
    InstaGallery,
    PartnerLogo,
    FooterComponent
  }
}
</script>

