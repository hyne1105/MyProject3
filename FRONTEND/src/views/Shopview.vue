<script>
import SliderShop from '@/components/SliderShop.vue'
import HeaderShop from '@/components/HeaderShop.vue'
import FooterShop from '@/components/FooterShop.vue'
import ProductService from '../services/Product.service'
import { mapState } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
import toastsVue from '../components/toasts.vue';
export default {
    data() {
        return {
            Products: [],
        }
    },
    components: {
        HeaderShop,
        SliderShop,
        toastsVue,
        FooterShop
    },
    computed: {
        ...mapState(useAuthStore, {
            currentUser: "user",
        }),
    },
    methods: {
        async retrieveProduct() {
            try {
                this.Products = await ProductService.getAll();
            } catch (error) {
                console.log(error);
            }
        },
    },
    mounted() {
        this.retrieveProduct();
    },
}
</script>
<template>
    <div class="header">
        <HeaderShop></HeaderShop>
    </div>
    <toastsVue></toastsVue>
    <div style="margin-top: 20px;">
        <div class="container">
            <div class="slider">
                <SliderShop></SliderShop>
            </div>
        </div>
    </div>

    <div class="container-fluid py-5">
        <div class="container">
            <div class="mx-auto text-center wow fadeIn" data-wow-delay="0.1s" style="max-width: 600px;">
                <h2 class="text-primary mb-3"><span class="fw-light text-dark">Sản Phẩm Của</span> Green</h2>
                <p class="mb-4">Mang màu xanh đến cho ngôi nhà, nơi làm việc hoặc không gian yêu thích của bạn.</p>
            </div>

            <div class="row g-4" id="giay">
                <div class="col-md-6 col-lg-3 wow fadeIn" data-wow-delay="0.1s" v-for="item in Products"
                    v-show="item.categories === 'Sen đá' || item.categories === 'Cây dây leo' || item.categories === 'Cây cảnh văn phòng' || item.categories === 'Xương rồng'">
                    <div class="product-item text-center p-4">
                        <div class="image_item" v-for="img in item.img">
                            <img :src="img" class="card-img-top img-fluid mb-4" alt="..." @click="nextdetailsproduct">
                        </div>
                        <div class="mb-2">
                            <small class="fa fa-star text-primary"></small>
                            <small class="fa fa-star text-primary"></small>
                            <small class="fa fa-star text-primary"></small>
                            <small class="fa fa-star text-primary"></small>
                            <small class="fa fa-star text-primary"></small>
                        </div>
                        <h5 class="card-title text-center mb-2 h6 d-inline-block">{{ item.title }}</h5>
                        <h5 class="text-primary mb-3">{{ item.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} VNĐ</h5>
                        <router-link :to="{ name: 'details', params: { id: item._id }, }" style="text-decoration: none;">
                            <div class="d-grid">
                                <button type="button" class="button-33" role="button" @click="nextdetailsproduct">Xem chi
                                    tiết</button>
                            </div>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Product End -->

    <div class="footer">
        <FooterShop></FooterShop>
    </div>
</template>
<style scoped>
.section-title {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
}

/*** Product ***/
.product-item {
    transition: .1s;
    border: 1px solid rgba(169, 169, 169, 0.662);
}

.product-item:hover {
    border-width: 0 !important;
    box-shadow: 0 0 35px rgba(144, 188, 121, .25);
}

.product-item:hover a.btn {
    color: var(--bs-white);
    background: var(--bs-primary);
}

.text-primary {
    color: #00b214 !important;
}
</style>