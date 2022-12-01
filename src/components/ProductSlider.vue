<template>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                <div class="col-lg-12 mt-5" v-if="(products.length > 0)">
                    <Carousel class="product-slider" :items-to-show="3" :autoplay="3000" :wrap-around="false" :transition="2000">
                        <Slide class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                            <div class="pi-pic"  >
                                <div v-if="(itemProduct.galleries.length > 0)">
                                    <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                </div>
                                <div v-else>
                                    <img src="img/logo2.png" alt="" />
                                </div>
                                <ul>
                                    <li  @click="saveKeranjang(itemProduct.id, itemProduct.name, itemProduct.price, (itemProduct.galleries.length > 0? itemProduct.galleries[0].photo : 'img/logo2.png'))" class="w-icon active">
                                        <a href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <li class="quick-view"><router-link v-bind:to="'/product/'+itemProduct.id">+ Quick View</router-link></li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{ itemProduct.type }}</div>
                                <a href="#">
                                    <h5>{{ itemProduct.name }}</h5>
                                </a>
                                <div class="product-price">
                                    {{ itemProduct.price }}
                                    <span>$35.00</span>
                                </div>
                            </div>
                        </Slide>
                        <template #addons>
                            <Navigation />
                            <Pagination />
                        </template>
                    </Carousel>
                </div>

                <div class="col-lg-12" v-else>
                    <p>
                        Produk terbaru belum tersedia untuk saat ini.
                    </p>
                </div>
            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
</template>

<script>

import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Pagination, Navigation} from 'vue3-carousel';
import axios from "axios";

export default {
  name: 'ProductSlider',
  components: {
    Carousel,
    Slide,
    Pagination,
    Navigation
  },
  data() {
    return {
        products: [],
        keranjangUser: []
    };
  },
  methods: {
    saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct){
        var productStored = {
            'id': idProduct,
            'name': nameProduct,
            'price': priceProduct,
            'photo': photoProduct
        }
        this.keranjangUser.push(productStored);
        console.log(this.keranjangUser);
        const parsed = JSON.stringify(this.keranjangUser);
        localStorage.setItem('keranjangUser', parsed);

        window.location.reload();
    }
  },
  mounted() {
    if(localStorage.getItem('keranjangUser')) {
        try {
            this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
        } catch (error) {
            localStorage.removeItem('keranjangUser');
        }
    }
    axios
        .get("http://127.0.0.1:8000/api/products")
        .then(res => (this.products = res.data.data.data))
        .catch(err => console.log(err));
  }
}
</script>

<style>
.product-item {
    display: flex;
    flex-direction: column;
}
.product-item .pi-pic {
    width: 90%;
}

</style>