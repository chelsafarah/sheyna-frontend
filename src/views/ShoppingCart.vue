<template>
    <div class="shopping">
      <HeaderComponent />

      <!-- Breadcrumb Section Begin -->
        <div class="breacrumb-section text-left">
            <div class="container">
                <div class="row">
                    <div class="col-lg-12">
                        <div class="breadcrumb-text product-more">
                            <router-link to="/">
                                <i class="fa fa-home"></i> Home
                            </router-link>
                            <span>Shopping Cart</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- Breadcrumb Section Begin -->

        <!-- Shopping Cart Section Begin -->
        <section class="shopping-cart spad">
            <div class="container">
                <div class="row">
                    <div class="col-lg-8">
                        <div class="row">
                            <div class="col-lg-12">
                                <div class="cart-table">
                                    <table>
                                        <thead>
                                            <tr>
                                                <th>Image</th>
                                                <th class="p-name text-center">Product Name</th>
                                                <th>Price</th>
                                                <th>Action</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr v-for="product in keranjangUser" :key="product.id">
                                                <td class="cart-pic first-row">
                                                    <img class="img-card" :src="product.photo" />
                                                </td>
                                                <td class="cart-title first-row text-center">
                                                    <h5>{{ product.name }}</h5>
                                                </td>
                                                <td class="p-price first-row">${{ product.price }}</td>
                                                <td class="delete-item"><a @click="removeItem(keranjangUser.index)" href="/cart"><i class="material-icons">
                                                close
                                                </i></a></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                            <div class="col-lg-8">
                                <h4 class="mb-4 text-left">
                                    Informasi Pembeli:
                                </h4>
                                <div class="user-checkout text-left">
                                    <form>
                                        <div class="form-group">
                                            <label for="namaLengkap">Nama lengkap</label>
                                            <input type="text" class="form-control" id="namaLengkap" aria-describedby="namaHelp" placeholder="Masukan Nama"
                                            v-model="customerInfo.name">
                                        </div>
                                        <div class="form-group">
                                            <label for="namaLengkap">Email Address</label>
                                            <input type="email" class="form-control" id="emailAddress" aria-describedby="emailHelp" placeholder="Masukan Email" v-model="customerInfo.email">
                                        </div>
                                        <div class="form-group">
                                            <label for="namaLengkap">No. HP</label>
                                            <input type="text" class="form-control" id="noHP" aria-describedby="noHPHelp" placeholder="Masukan No. HP" v-model="customerInfo.number">
                                        </div>
                                        <div class="form-group">
                                            <label for="alamatLengkap">Alamat Lengkap</label>
                                            <textarea class="form-control" id="alamatLengkap" rows="3" v-model="customerInfo.address"></textarea>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-lg-4">
                        <div class="row">
                            <div class="col-lg-12">
                                <div class="proceed-checkout text-left">
                                    <ul>
                                        <li class="subtotal">ID Transaction <span>#SH12000</span></li>
                                        <li class="subtotal mt-3">Subtotal <span>${{ totalPrice }}.00</span></li>
                                        <li class="subtotal mt-3">Pajak <span>10% ${{ tax }}.00</span></li>
                                        <li class="subtotal mt-3">Total Biaya <span>${{ totalPay }}.00</span></li>
                                        <li class="subtotal mt-3">Bank Transfer <span>Mandiri</span></li>
                                        <li class="subtotal mt-3">No. Rekening <span>2208 1996 1403</span></li>
                                        <li class="subtotal mt-3">Nama Penerima <span>Shayna</span></li>
                                    </ul>
                                    <!-- <router-link to="/success" href="success.html" class="proceed-btn">I ALREADY PAID</router-link> -->
                                    <a @click="checkout()" href="#" class="proceed-btn">I ALREADY PAID</a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <!-- Shopping Cart Section End -->

    </div>
  </template>
  
  <script>
  // @ is an alias to /src
  // import HelloWorld from '@/components/HelloWorld.vue'
  import HeaderComponent from '@/components/HeaderComponent.vue';
  import axios from "axios";

  export default {
    name: 'ShoppingCart',
    components: {
      HeaderComponent,
    },
    data() {
        return {
            keranjangUser: [],
            customerInfo: {
                name : '',
                email : '',
                number : '',
                address : '',
            }
        }
    },
    methods: {
        removeItem(index) {
            this.keranjangUser.splice(index, 1);
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
        },

        checkout(){
            let productIds = this.keranjangUser.map(function(product){
                return product.id
            });

            let checkoutData = {
                "name" : this.customerInfo.name,
                "email" : this.customerInfo.email,
                "number" : this.customerInfo.number,
                "address" : this.customerInfo.address,
                "transaction_total" : this.totalPay,
                "transaction_status" : "PENDING",
                "transaction_details" : productIds
            };

            axios
                .post("http://127.0.0.1:8000/api/checkout", checkoutData)
                .then(() => this.$router.push("success"))
                .catch(err => console.log(err));
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
    },
    computed: {
        totalPrice() {
            return this.keranjangUser.reduce(function(items, data){
                return items + data.price;
            }, 0)
        },
        tax() {
            return (this.totalPrice * 10) / 100;
        },
        totalPay() {
            return this.totalPrice + this.tax;
        }
    }

  }
  </script>

<style scoped>
    .img-card {
        width: 100px;
        height: 100px;
    }
</style>
  
  