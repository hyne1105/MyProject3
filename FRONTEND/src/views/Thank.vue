<script>
import HeaderShop from '@/components/HeaderShop.vue'
import FooterShop from '@/components/FooterShop.vue' 
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

    <div class="container d-flex justify-content-center">
        <div class="card1">
            <div class="circle"></div>
            <div class="circle"></div>
            <div class="card-inner">
                <div class="thanks text-center">CẢM ƠN VÌ ĐÃ ĐẶT HÀNG</div>
            </div>
        </div>
    </div>

    <FooterShop></FooterShop>
</template>
<style scoped>
.card1 {
    margin: 50px;
    width: 800px;
    height: 200px;
    transition: all 0.2s;
    position: relative;
    cursor: pointer;
}

.card-inner {
    width: inherit;
    height: inherit;
    background: rgba(255, 255, 255, 0.197);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
    backdrop-filter: blur(10px);
    border-radius: 8px;
}
.thanks{
    color: #00b214;
    padding-top: 60px;
    font-size: 40px;
    margin: auto;
    font-weight: 600;
    font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}
.card1:hover {
    transform: scale(1.04) rotate(1deg);
}

.circle {
    width: 100px;
    height: 100px;
    background: radial-gradient(#b0e633, #53ef7d);
    border-radius: 50%;
    position: absolute;
    animation: move-up6 1s ease-in infinite alternate-reverse;
}

.circle:nth-child(1) {
    top: -25px;
    left: -25px;
}

.circle:nth-child(2) {
    bottom: -25px;
    right: -25px;
    animation-name: move-down1;
}

@keyframes move-up6 {
    to {
        transform: translateY(-10px);
    }
}

@keyframes move-down1 {
    to {
        transform: translateY(10px);
    }
}
</style>