<script>
import UserService from "../services/User.service";
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
        users: Array,
        refeshlist: Function,
        activeUser: { type: Number, default: -1 },
    },
    emits: ['update:activeUser'],
    methods: {
        toastjs,
        async deluser(id) {
            try {
                await UserService.delete(id);
                this.refeshlist();
                this.toasts.title = "Success",
                    this.toasts.msg = "Đã xóa người dùng",
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
        updateuserindex(index) {
            this.$emit("update:activeUser", index)
        }
    }
}
</script>
<template>
    <div class="container mt-3">
        <h2>Danh sách người dùng</h2>
        <p>Tất cả tài khoản người dùng của GREEN. Không được tùy tiện xóa bỏ</p>
        <table class="table shadow-sm p-3 mb-5 bg-body rounded">
            <thead>
                <tr>
                    <th class="col-5">Tên tài khoản</th>
                    <th class="col-6">Email</th>
                    <th class="text-center col-1">Xóa</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>
                        <li class="user-item d-flex justify-content-between py-2" v-for="(user, index) in users" v-show="!user.isAdmin" :key="user._id" @click="updateuserindex(index)">
                            <span>{{ user.username }}</span>
                        </li>
                    </td>
                    <td>
                        <li class="user-item d-flex justify-content-between py-2" v-for="(user, index) in users" v-show="!user.isAdmin" :key="user._id" @click="updateuserindex(index)">
                            <span>{{ user.email }}</span>
                        </li>
                    </td>
                    <td>
                        <div>
                            <li class="user-item1 d-flex justify-content-between py-2">
                                <div class="bi bi-trash3-fill" @click="deluser(user._id)"></div>
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
    padding-left: 20px;
}
</style>