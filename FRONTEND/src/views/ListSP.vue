<script>
import AdminHeader from "../components/AdminHeader.vue";
import ListUser from "../components/ListUser.vue";
import UserService from "../services/User.service";
import toastsVue from "../components/toasts.vue";
import ProductService from "../services/Product.service";
import ListProduct from "../components/ListProduct.vue";
import Productcard from "../components/Productcard.vue";
import Usercard from "../components/Usercard.vue";
import toast from "../assets/js/toasts";
export default {
    data() {
        return {
            users: [],
            products: [],
            activeIndex: -1,
            activeUser: -1,
            toasts: {
                title: "Warning",
                msg: "Bạn không phải ADMIN",
                type: "warn",
                duration: 3000
            },
        }
    },
    computed: {
        getindex() {
            if (this.activeIndex != -1) {
                const list = document.querySelectorAll(".product-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeIndex].classList.add("active");
                return this.products[this.activeIndex];
            }
        },
        getindexuser() {
            if (this.activeUser != -1) {
                const list = document.querySelectorAll(".user-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeUser].classList.add("active");
                return this.users[this.activeUser];
            }
        }
    },
    components: {
        AdminHeader,
        ListUser,
        ListProduct,
        toastsVue,
        Productcard,
        Usercard
    },
    methods: {
        toast,
        async getall() {
            try {
                this.products = await ProductService.getAll();
                this.users = await UserService.getAll();
            } catch (error) {
                console.log(error);
                this.toast();
                setTimeout(() => {
                    this.$router.push({ name: "ShopMain" });
                }, 1000);
            }
        },
    },
    created() {
        this.getall();
    },
}
</script>

<template>
    <AdminHeader></AdminHeader>
    <div class="header">
        <div class="py-2 text-end px-4">QUẢN LÝ SẢN PHẨM</div>
    </div>

    <div class="container row pb-5" style="margin-left: 120px;">
        <div class="list-product col-9">
            <div>
                <ListProduct :products="products" :refeshlist="getall" :getindex="getindex"
                    v-model:activeIndex="activeIndex"></ListProduct>
                <router-link to="/addproduct" style="padding-left: 15px;">
                    <button class="my-button">Thêm sản phẩm</button>
                </router-link>
            </div>

        </div>
        <div class="pos col-3">
            <div class="list_item_product">
                <div>

                    <div class="card_product" style="padding: 10px;" v-if="getindex">
                        <Productcard :products="getindex"></Productcard>
                        <router-link :to="{ name: 'editproduct', params: { id: getindex._id }, }"
                            style="text-decoration: none;">
                            <div class="col-3 pt-4">
                                <button class="Btn">
                                    <div style="font-size: 10px; text-decoration: none;">Chỉnh sửa</div>
                                    <svg class="svg" viewBox="0 0 512 512">
                                        <path
                                            d="M410.3 231l11.3-11.3-33.9-33.9-62.1-62.1L291.7 89.8l-11.3 11.3-22.6 22.6L58.6 322.9c-10.4 10.4-18 23.3-22.2 37.4L1 480.7c-2.5 8.4-.2 17.5 6.1 23.7s15.3 8.5 23.7 6.1l120.3-35.4c14.1-4.2 27-11.8 37.4-22.2L387.7 253.7 410.3 231zM160 399.4l-9.1 22.7c-4 3.1-8.5 5.4-13.3 6.9L59.4 452l23-78.1c1.4-4.9 3.8-9.4 6.9-13.3l22.7-9.1v32c0 8.8 7.2 16 16 16h32zM362.7 18.7L348.3 33.2 325.7 55.8 314.3 67.1l33.9 33.9 62.1 62.1 33.9 33.9 11.3-11.3 22.6-22.6 14.5-14.5c25-25 25-65.5 0-90.5L453.3 18.7c-25-25-65.5-25-90.5 0zm-47.4 168l-144 144c-6.2 6.2-16.4 6.2-22.6 0s-6.2-16.4 0-22.6l144-144c6.2-6.2 16.4-6.2 22.6 0s6.2 16.4 0 22.6z">
                                        </path>
                                    </svg>
                                </button>
                            </div>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <toastsVue></toastsVue>
</template>
<style scoped>
.header {
    background-color: rgb(57, 151, 107);
    color: white;
    font-size: 25px;
}

.list-product {
    width: 900px;
    min-height: 700px;
    margin-top: 30px;
    padding-left: 80px;
}

.list_item_product {
    width: 200px;
    max-height: 150px;
}

.pos {
    padding-top: 100px;
    padding-left: 100px;

}
</style>