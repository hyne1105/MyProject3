<script>
import OrderService from "../services/Order.service";
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
        orders: Array,
        refeshlist: Function,
        activeOrder: { type: Number, default: -1 },
    },
    emits: ['update:activeOrder'],
    methods: {
        toastjs,
        async delorder(id) {
            try {
                await OrderService.delete(id);
                this.refeshlist();
                this.toasts.title = "Success",
                    this.toasts.msg = "Đã xóa đơn hàng",
                    this.toasts.type = "success",
                    this.toasts.duration = 2000
                this.toastjs();
            } catch (error) {
                console.log(error);
                this.toasts.title = "Warning",
                    this.toasts.msg = "Tài khoản không phải ADMIN",
                    this.toasts.type = "warn",
                    this.toasts.duration = 2000
                this.toastjs();
            }
        },
        updateorderindex(index) {
            this.$emit("update:activeOrder", index)
        }
    }
}
</script>
<template>
    <div class="container mt-3">
        <h2>Danh sách đơn hàng</h2>
        <p>Tất cả đơn hàng người dùng của GREEN. Không được tùy tiện xóa bỏ</p>
        <table class="table shadow-sm p-3 mb-5 bg-body rounded">
            <thead>
                <tr>
                    <th class="">Mã người dùng</th>
                    <th class="">Số lượng</th>
                    <th class="">Cách thức giao hàng</th>
                    <th class="">Trạng thái</th>
                    <th class="text-center">Xóa</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(order, index) in orders" :key="order._id">
                    <td>
                        <li class="user-item d-flex justify-content-between py-2" >
                            <span>{{ order.userId }}</span>
                        </li>
                    </td>
                    <!-- <td>
                        <li class="user-item d-flex justify-content-between py-2" >
                            <span>{{ order.productId }}</span>
                        </li>
                    </td> -->
                    <td>
                        <li class="user-item d-flex justify-content-between py-2" >
                            <span>{{ order.quantity }}</span>
                        </li>
                    </td>
                    <td>
                        <li class="user-item d-flex justify-content-between py-2" >
                            <span>{{ order.address }}</span>
                        </li>
                    </td>
                    <td>
                        <li class="user-item d-flex justify-content-between py-2" >
                            <span>{{ order.status }}</span>
                        </li>
                    </td>
                    <td>
                        <div>
                            <li class="user-item1 d-flex justify-content-between py-2">
                                <div class="bi bi-trash3-fill" @click="delorder(order._id)"></div>
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

td .user-item1{
    padding-left: 60px;
}
</style>