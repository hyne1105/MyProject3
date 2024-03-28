<script>
import ProductService from "../services/Product.service";
import toastjs from "../assets/js/toasts";
export default {
    data() {
        return {
            toasts: {
                title: "",
                msg: "",
                type: "",
                duration: 0
            },
        }
    },
    props: {
        products: Array,
        refeshlist: Function,
        activeIndex: { type: Number, default: -1 },
    },
    emits: ["update:activeIndex"],
    methods: {
        toastjs,
        async delproduct(id) {
            try {
                await ProductService.delete(id);
                this.refeshlist();
                this.toasts.title = "Success",
                    this.toasts.msg = "Đã xóa sản phẩm",
                    this.toasts.type = "success",
                    this.toasts.duration = 2000
                this.toastjs();
            } catch (error) {
                console.log(error);
                this.toasts.title = "Warning",
                    this.toasts.msg = "Bạn chưa đăng nhập hoặc bạn không phải ADMIN",
                    this.toasts.type = "warn",
                    this.toasts.duration = 2000
                this.toastjs();
            }
        },
        updateActiveIndex(index) {
            this.$emit("update:activeIndex", index);
        },
    }
}
</script>
<template>
    <div class="container mt-3">
        <h2>Danh sách sản phẩm</h2>
        <p>Tất cả sản phẩm của GREEN. Không được tùy tiện xóa bỏ</p>
        <table class="table shadow-sm p-3 mb-5 bg-body rounded">
            <thead>
                <tr>
                    <th class="">Tên sản phẩm</th>
                    <th class="">Giá</th>
                    <th class="">Kích thước</th>
                    <th class="">Màu chậu</th>
                    <th class="text-center">Xóa</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(product, index) in products" :key="product._id" @click="updateActiveIndex(index)">
                    <td>
                        <li class="user-item product-item d-flex justify-content-between py-2">
                            <span>{{ product.title }}</span>
                        </li>
                    </td>
                    <td>
                        <li class="user-item product-item d-flex justify-content-between py-2">
                            <span>{{ product.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }}</span>
                        </li>
                    </td>
                    <td>
                        <li class="user-item product-item d-flex justify-content-between py-2">
                            <span>{{ product.size }}</span>
                        </li>
                    </td>
                    <td>
                        <li class="user-item product-item d-flex justify-content-between py-2">
                            <span>{{ product.color }}</span>
                        </li>
                    </td>
                    <td>
                        <div>
                            <li class="user-item1 product-item d-flex justify-content-between py-2">
                                <div class="bi bi-trash3-fill" @click="delproduct(product._id)"></div>
                            </li>
                        </div>

                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<style scoped>
td .user-item:hover {
    background-color: #04c668f7;
    color: white;
}

td .user-item1:hover {
    background-color: #c60404c0;
    color: white;
}

td .user-item1 {
    padding-left: 60px;
}
</style>