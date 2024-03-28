<script>
import AdminHeader from "../components/AdminHeader.vue";
import toastsVue from "../components/toasts.vue";
import toast from "../assets/js/toasts";
import OrderService from "../services/Order.service";
import ListOrder from "../components/ListOrder.vue";
export default {
    data() {
        return {
            users: [],
            products: [],
            orders: [],
            activeIndex: -1,
            activeUser: -1,
            activeOrder: -1,
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
        },
        getindexorder() {
            if (this.activeOrder != -1) {
                const list = document.querySelectorAll(".order-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeOrder].classList.add("active");
                return this.orders[this.activeOrder];
            }
        }
    },
    components: {
        AdminHeader,
        ListOrder,
        toastsVue,
    },
    methods: {
        toast,
        async getall() {
            try {
                this.orders = await OrderService.getAll();
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
        console.log(this.orders);
    },
}
</script>

<template>
    <AdminHeader></AdminHeader>
    <div>
        <div class="header">
            <div class="py-2 text-end px-4">QUẢN LÝ ĐƠN HÀNG</div>
        </div>
        <div class="container row pb-5" style="margin-left: 120px;">
            <div class="list-order col-10">
                <div>
                    <ListOrder :orders="orders" :refeshlist="getall" v-model:activeOrder="activeOrder"></ListOrder>
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

.list-order {
    width: 1400px;
    min-height: 700px;
    margin-top: 30px;
    padding-left: 100px;
}

</style>