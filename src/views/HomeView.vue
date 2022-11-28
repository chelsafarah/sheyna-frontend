<template>
  <div class="home">
    <HeaderComponent />
    <!-- Hero Section Begin -->
    <section class="hero-section">
        <Carousel :items-to-show="1" :autoplay="2000" :wrap-around="true">
            <Slide class="single-hero-items set-bg" style="background-image: url('img/hero-1.jpg')">
                <div class="container">
                    <div class="row">
                        <div class="col-lg-5">
                            <span>Bag,kids</span>
                            <h1>Black friday</h1>
                            <p>
                                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore
                            </p>
                            <a href="#" class="primary-btn">Shop Now</a>
                        </div>
                    </div>
                </div>
            </Slide>
            <Slide class="single-hero-items set-bg" style="background-image: url('img/hero-2.jpg')">
                <div class="container">
                    <div class="row">
                        <div class="col-lg-5">
                            <span>Bag,kids</span>
                            <h1>Black friday</h1>
                            <p>
                                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore
                            </p>
                            <a href="#" class="primary-btn">Shop Now</a>
                        </div>
                    </div>
                </div>
            </Slide>
            <Slide class="single-hero-items set-bg" style="background-image: url('img/hero-3.jpg')">
                <div class="container">
                    <div class="row">
                        <div class="col-lg-5">
                            <span>Bag,kids</span>
                            <h1>Black friday</h1>
                            <p>
                                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore
                            </p>
                            <a href="#" class="primary-btn">Shop Now</a>
                        </div>
                    </div>
                </div>
            </Slide>
            <template #addons>
              <Navigation />
              <Pagination />
            </template>
        </Carousel>
    </section>
    <!-- Hero Section End -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderComponent from '@/components/HeaderComponent.vue';
import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide, Pagination, Navigation} from 'vue3-carousel'

export default {
  name: 'HomeView',
  components: {
    HeaderComponent,
    Carousel,
    Slide,
    Pagination,
    Navigation
  }
}
</script>

<style>
.set-bg {
    width: 100%;
    height: 500px;
}
</style>

