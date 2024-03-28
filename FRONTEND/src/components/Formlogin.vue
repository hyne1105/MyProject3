<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
import { mapActions } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
import toast from "../assets/js/toasts";
export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const Loginform = yup.object().shape({
      username: yup
        .string()
        .required("Tên phải có giá trị.")
        .min(2, "Tên phải ít nhất 2 ký tự."),
      password: yup
        .string()
        .required("Mật khẩu phải có giá trị.")
    });
    return {
      Loginform,
      toasts: {
        title: "Warning",
        msg: "Tên đăng nhập hoặc tài khoản không đúng!",
        type: "warn",
        duration: 2000
      },
    }
  },
  methods: {
    toast,
    showPwd() {
      if (document.querySelector("#checkpwd").checked == true) {
        document.querySelector("#pwd").type = 'text';
      } else {
        document.querySelector("#pwd").type = 'password';
      }
    },
    ...mapActions(useAuthStore, ["login"]),
    async handleLogin(user) {
      try {
        await this.login(user);
        location.href = 'http://localhost:8001/';
      } catch (error) {
        this.toast();
        console.log(error);
      }
    },
  },
};
</script>
<template>
  <Form :validation-schema="Loginform" @submit="handleLogin">
    <div class="form-outline mb-4">
      <label class="form-label label1 fw-bold" for="username">Tên đăng nhập</label>
      <Field id="name" placeholder="Nhập tên đăng nhập" name="username" type="text" class="form-control" />
      <ErrorMessage name="username" class="label1"/>
    </div>

    <!-- Password input -->
    <div class="form-outline mb-3">
      <label class="form-label label1 fw-bold" for="pwd">Mật khẩu</label>
      <Field id="pwd" placeholder="Nhập mật khẩu" name="password" type="password" class="form-control" />
      <ErrorMessage name="password" class="label1" />

    </div>
    <div class="">
      <!-- Checkbox -->
      <div class="form-check mb-0 label1">
        <input class="form-check-input me-2 " type="checkbox" value="" id="checkpwd" @click="showPwd()" />
        <label class="form-check-label" for="checkpwd">
          Hiện mật khẩu
        </label>
      </div>
    </div>
    <div class="text-center t-lg-start mt-4 pt-2 ">
      <button class="my-button">Đăng Nhập</button>
      <div class="hr"></div>
      <p class="text-white">Bạn chưa có tài khoản ? <router-link to="/logup" style="text-decoration: none; color: white; font-weight: bold;"> Đăng Ký</router-link></p>
    </div>
  </Form>
</template>

<style>
.login-wrap {
    width: 100%;
    margin: auto;
    max-width: 450px;
    min-height: 550px;
    position: relative;
    background: url(https://media.licdn.com/dms/image/D5612AQFoSspOIiDxiQ/article-cover_image-shrink_600_2000/0/1664099773634?e=2147483647&v=beta&t=1Tpxqag6iAcbsSyDI8redYKFp4UxqT8tnFGtXpiJiDs) no-repeat center;
    box-shadow: 0 12px 15px 0 rgba(0, 0, 0, .24), 0 17px 50px 0 rgba(0, 0, 0, .19);
}

.login-html {
    width: 100%;
    height: 100%;
    position: absolute;
    padding-top: 60px;
    background: rgba(100, 109, 101, 0.577);
}

.hr {
    height: 2px;
    margin: 20px 0 30px 0;
    background: rgba(208, 207, 207, 0.2);
} 

.form-check-input:checked {
  background-color: #00b214;
  border-color: #00b214;
}

.form-control {
  width: 80%;
  margin-left: 10%;
}

.label1 {
  margin-left: 10%;
  color: white;
}

</style>