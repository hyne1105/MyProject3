
<script>
import AdminHeader from "../components/AdminHeader.vue";
import toastjs from "../assets/js/toasts";
import toastsVue from "../components/toasts.vue";
import ProductService from "../services/Product.service";
import Productform from "../components/Productform.vue";
export default {
    data() {
        return {
            toasts: {
                title: "Success",
                msg: "Thêm sản phẩm thành công",
                type: "success",
                duration: 2000
            },
        }
    },
    components: {
        AdminHeader,
        Productform,
        toastsVue
    },
    methods: {
        toastjs,
        async addproduct(data) {
            try {
                await ProductService.create(data);
                this.toastjs();
                setTimeout(() => {
                    location.reload();
                }, 2000);
            } catch (error) {
                console.log(error);
                this.toasts.title = "Warning",
                    this.toasts.msg = "Tài khoản không phải ADMIN",
                    this.toasts.type = "warn",
                    this.toasts.duration = 2000
                this.toastjs();
            }
        },
    },
};
</script>
<template>
    <AdminHeader></AdminHeader>
    <div>
        <div class="header">
            <div class="py-2 text-end px-4">THÊM SẢN PHẨM</div>
        </div>
        <Productform :product="{ img: [] }" @submit:product="addproduct" :resetAfterSubmit="false" />
    </div>
    <toastsVue></toastsVue>
</template>

<style>
.header {
    background-color: rgb(57, 151, 107);
    color: white;
    font-size: 25px;
}
</style>
