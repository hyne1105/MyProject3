<script>
import HeaderShop from '@/components/HeaderShop.vue'
import FooterShop from '@/components/FooterShop.vue';
import ProductService from '../services/Product.service'
import CartService from '../services/Cart.service'
import toastsVue from '../components/toasts.vue'
import toastsjs from '../assets/js/toasts.js'
import { mapState } from 'pinia'
import { useAuthStore } from "@/stores/Auth.store";
export default {
    data() {
        return {
            detailproduct: [],
            cartitem: {
                userId: '',
                productId: this.$route.params.id,
                quantity: 1,
                title: "",
                img: "",
                price: "",
                size: "",
                color: "",
            },
            carts: [],
            toasts: {
                // title: "THÊM VÀO GIỎ HÀNG THÀNH CÔNG",
                // msg: "+1 sp",
                // type: "success",
                // duration: 2000
            },
            sub_quantity: 1,
        }
    },
    computed: {
        ...mapState(useAuthStore, {
            currentUser: "user",
        }),
    },
    components: {
        HeaderShop,
        toastsVue,
        FooterShop,
    },
    methods: {
        toastsjs,
        async getproduct() {
            try {
                this.detailproduct = await ProductService.get(this.$route.params.id);
                this.cartitem.title = this.detailproduct.title;
                this.cartitem.img = this.detailproduct.img[0];
                this.cartitem.price = this.detailproduct.price;
                this.cartitem.size = this.detailproduct.size;
                this.cartitem.color = this.detailproduct.color;
            } catch (error) {
                console.log(error);
            }
        },
        async getidcart() {
            this.cartitem.quantity = this.sub_quantity;
            var exitcart = false;

            try {
                this.carts = await CartService.get(this.currentUser._id);
                this.cartitem.userId = this.currentUser._id;
                this.carts.map((cartproduct) => {
                    if (cartproduct.productId == this.cartitem.productId) {
                        this.cartitem.quantity += cartproduct.quantity;
                        CartService.update(cartproduct._id, this.cartitem);
                        exitcart = true;
                        this.toastsjs();
                        setTimeout(() => {
                            this.$router.push({ name: 'CartShop' });
                        }, 1000);
                    }
                })
                if (exitcart === false) {
                    this.cartitem.userId = this.currentUser._id;
                    CartService.create(this.cartitem);
                    this.toastsjs();
                    setTimeout(() => {
                        this.$router.push({ name: 'CartShop' });
                    }, 1000);
                }
            } catch (error) {
                // this.toasts.title = "Message",
                this.toasts.msg = "ĐĂNG NHẬP ĐỂ MUA HÀNG",
                    this.toasts.type = "warn",
                    this.toasts.duration = 3000,
                    this.toastsjs();
                console.log(error);
            }
        },
    },
    created() {
        this.getproduct();
    },

}
</script>
<template>
    <HeaderShop></HeaderShop>

    <toastsVue></toastsVue>
    <div class="wrapper container shadow-sm p-3 mb-5 bg-body rounded pb-5">
        <div class="row pt-5">
            <div class="col d-flex justify-content-center">
                <div id="carouselExampleControls" data-bs-ride="carousel">
                    <div>
                        <div v-for="(img, index) in detailproduct.img" :class="{ active: index == 0 }">
                            <img :src="img" class="" alt="..." style="width: 300px;">
                        </div>
                    </div>
                </div>
            </div>
            <div class="col" style="margin-right: 50px;">
                <h4 style="font-weight: 600;">{{ detailproduct.title }}</h4>

                <div class="mb-2">
                    <small class="fa fa-star text-primary"></small>
                    <small class="fa fa-star text-primary"></small>
                    <small class="fa fa-star text-primary"></small>
                    <small class="fa fa-star text-primary"></small>
                    <small class="fa fa-star text-primary"></small>
                </div>

                <h5>{{ detailproduct.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} VNĐ</h5>


                <p>{{ detailproduct.desc }}</p>
                <h6>Kích thước: {{ detailproduct.size }}</h6>
                <div class="color_product">
                    <h6>Màu chậu: {{ detailproduct.color }} </h6>
                </div>
                <div class="row">
                    <h6 class="col-2 tquan">Số lượng</h6>
                    <input id="quantity" name="quantity" type="number" v-model="sub_quantity" class="formcontrol col-10"
                        style="width:50px; border: none;" />
                </div>

            </div>
            <div class="btn_product">
                <router-link to="/">
                    <button class="button2">
                        <div class="button-box">
                            <span class="button-elem">
                                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 46 40">
                                    <path
                                        d="M46 20.038c0-.7-.3-1.5-.8-2.1l-16-17c-1.1-1-3.2-1.4-4.4-.3-1.2 1.1-1.2 3.3 0 4.4l11.3 11.9H3c-1.7 0-3 1.3-3 3s1.3 3 3 3h33.1l-11.3 11.9c-1 1-1.2 3.3 0 4.4 1.2 1.1 3.3.8 4.4-.3l16-17c.5-.5.8-1.1.8-1.9z">
                                    </path>
                                </svg>
                            </span>
                            <span class="button-elem">
                                <svg viewBox="0 0 46 40">
                                    <path
                                        d="M46 20.038c0-.7-.3-1.5-.8-2.1l-16-17c-1.1-1-3.2-1.4-4.4-.3-1.2 1.1-1.2 3.3 0 4.4l11.3 11.9H3c-1.7 0-3 1.3-3 3s1.3 3 3 3h33.1l-11.3 11.9c-1 1-1.2 3.3 0 4.4 1.2 1.1 3.3.8 4.4-.3l16-17c.5-.5.8-1.1.8-1.9z">
                                    </path>
                                </svg>
                            </span>
                        </div>
                    </button>
                </router-link>

                <button class="button1" type="submit" @click="getidcart()">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-3 h-3">
                        <path stroke-linecap="round" stroke-linejoin="round"
                            d="M4.5 12h15m0 0l-6.75-6.75M19.5 12l-6.75 6.75"></path>
                    </svg>
                    <div class="text1">
                        Đặt hàng
                    </div>
                </button>
            </div>
        </div>
    </div>

    <FooterShop></FooterShop>
</template>
<style scoped>
.text-primary {
    color: #00b214 !important;
}

.btn_product {
    display: flex;
    justify-content: space-around;
    padding-top: 30px;
}

.size_product,
.color_product {
    display: flex;
    flex-direction: column;
    max-width: 400px;
}

.list_btn_size,
.list_btn_color {
    margin: 0 10px;
    display: flex;
    flex-wrap: wrap;
}

.list_btn_size button,
.list_btn_color button {
    margin: 10px 5px;
}

.btn {
    width: 100px;
}

.wrapper {
    margin: 30px 100px;
    /* background-image: url("../assets/img/bg1.jpg"); */
    /* width: 1; */
    background-color: white;
    height: 500px;

}

.heading {
    margin: 0 100px;
}

.title {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    height: 100px;
}

.formcontrol {
    background-color: rgb(234, 237, 227);
}
</style>