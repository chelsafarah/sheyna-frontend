<template>
    <div class="product">
      <HeaderComponent />
        <!-- Breadcrumb Section Begin -->
        <div class="breacrumb-section text-left">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="breadcrumb-text product-more">
                            <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                            <span>Detail</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Breadcrumb Section Begin -->

        <!-- Product Shop Section Begin -->
        <section class="product-shop spad page-details">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="row">
                            <div class="col-lg-6">
                                <div class="product-pic-zoom">
                                    <div v-if="(photo_product != '')">
                                        <img class="product-big-img" :src="photo_product" alt="" />
                                    </div>
                                    <div v-else>
                                        <img class="product-big-img" src="img/logo2.png" alt="" />
                                    </div>
                                    
                                </div>
                                <div class="product-thumbs" v-if="(productDetails.galleries != null)">
                                    <Carousel class="product-thumbs-track ps-slider" :items-to-show="3" >
                                        <div v-for="gallery in productDetails.galleries" v-bind:key="gallery.id"> 
                                            <Slide class="pt" @click="changeImage(gallery.photo)" :class="gallery.photo == photo_product ? 'active' : '' ">
                                                <img v-bind:src="gallery.photo" alt="" />
                                            </Slide>
                                        </div>
                                    </Carousel>
                                </div>
                            </div>
                            <div class="col-lg-6">
                                <div class="product-details text-left">
                                    <div class="pd-title">
                                        <span>{{ productDetails.type }}</span>
                                        <h3>{{ productDetails.name }}</h3>
                                    </div>
                                    <div class="pd-desc">
                                        <p v-html="productDetails.description">
                                        </p>
                                        <h4>${{ productDetails.price }}</h4>
                                    </div>
                                    <div class="quantity">
                                        <router-link to="/cart" class="primary-btn pd-cart">Add To Cart</router-link>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Product Shop Section End -->
      <RelatedProduct />
      <FooterComponent /> 
    </div>
</template>
  
<script>
  // @ is an alias to /src
  // import HelloWorld from '@/components/HelloWorld.vue'
  import HeaderComponent from '@/components/HeaderComponent.vue';
  import RelatedProduct from '@/components/RelatedProduct.vue';
  import FooterComponent from '@/components/FooterComponent.vue';

  import 'vue3-carousel/dist/carousel.css';
  import { Carousel, Slide} from 'vue3-carousel'
  import axios from "axios";

  export default {
    name: 'ProductView',
    components: {
      HeaderComponent,
      Carousel,
      Slide,
      FooterComponent,
      RelatedProduct
    },
    data() {
        return {
            photo_product: "",
            productDetails: [],
        }
    },
    methods: {
        changeImage(urlImage) {
            this.photo_product = urlImage;
        },
        setData(data) {
            this.productDetails = data;
            this.photo_product = data.galleries[0].photo;
        }
    },
    mounted() {
    axios
        .get("http://127.0.0.1:8000/api/products", {
            params: {
                id: this.$route.params.id
            }
        })
        .then(res => (this.setData(res.data.data)))
        .catch(err => console.log(err));
    }
  }
</script>
  
<style scoped>
    .product-thumbs .pt{
        margin-right: 10px;
    }

    .product-big-img {
        max-width: 300px;
    }
</style>
  