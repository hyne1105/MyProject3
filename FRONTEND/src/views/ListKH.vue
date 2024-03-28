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
    <div>
        <div class="header">
            <div class="py-2 text-end px-4">QUẢN LÝ TÀI KHOẢN</div>
        </div>
        <div class="container row pb-5" style="margin-left: 120px;">
            <div class="list-account col-10">
                <div>
                    <ListUser :users="users" :refeshlist="getall" v-model:activeUser="activeUser"></ListUser>
                </div>

            </div>
            <div class="pos col-2">
                <div class="list_item_user" id="user">
                    <div v-if="getindexuser">
                        <div>
                            <Usercard :users="getindexuser" v-model:activeUser="activeUser"></Usercard>
                        </div>
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

.list-account {
    width: 1000px;
    min-height: 700px;
    margin-top: 30px;
    padding-left: 80px;
}


.list_item_user {
    width: 200px;
    max-height: 150px;
}


.pos {
    padding-top: 100px;
    padding-left: 90px;

}
</style>