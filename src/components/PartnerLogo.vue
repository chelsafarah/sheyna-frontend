<template>
    <!-- Partner Logo Section Begin -->
    <div class="partner-logo">
        <div class="container">
            <Carousel class="logo-carousel" :items-to-show="5" :autoplay="3000" :wrap-around="true">
                <Slide class="logo-item">
                    <div class="tablecell-inner">
                        <img src="img/logo-carousel/logo-1.png" alt="" />
                    </div>
                </Slide>
                <Slide class="logo-item">
                    <div class="tablecell-inner">
                        <img src="img/logo-carousel/logo-2.png" alt="" />
                    </div>
                </Slide>
                <Slide class="logo-item">
                    <div class="tablecell-inner">
                        <img src="img/logo-carousel/logo-3.png" alt="" />
                    </div>
                </Slide>
                <Slide class="logo-item">
                    <div class="tablecell-inner">
                        <img src="img/logo-carousel/logo-4.png" alt="" />
                    </div>
                </Slide>
                <Slide class="logo-item">
                    <div class="tablecell-inner">
                        <img src="img/logo-carousel/logo-5.png" alt="" />
                    </div>
                </Slide>
            </Carousel>
        </div>
    </div>
    <!-- Partner Logo Section End -->
</template>



<script>

import 'vue3-carousel/dist/carousel.css'
import { Carousel, Slide } from 'vue3-carousel'

export default {
  name: 'PartnerLogo',
  components: {
    Carousel,
    Slide,
  }
}
</script>