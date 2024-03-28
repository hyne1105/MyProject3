<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
import AuthService from "../services/Auth.service";
import toast from "../assets/js/toasts";
import toastsVue from "../components/toasts.vue";
import HeaderShop from "../components/HeaderShop.vue";
export default {
  components: {
    Form,
    Field,
    ErrorMessage,
    HeaderShop,
    toastsVue
  },
  data() {
    const Logupform = yup.object().shape({
      name: yup
        .string()
        .required("Tên phải có giá trị.")
        .min(2, "Tên phải ít nhất 2 ký tự."),
      email: yup
        .string()
        .required("Email phải có giá trị.")
        .email("E-mail không đúng.")
        .max(50, "E-mail tối đa 50 ký tự."),
      pwd: yup
        .string()
        .required("Mật khẩu phải có giá trị.")
    });
    return {
      Logupform,
      message: "Đăng ký thành công",
      usernew: {
        username: "",
        email: "",
        password: "",
      },
      toasts: {
        title: "",
        msg: "",
        type: "",
        duration: 0
      },
    };
  },
  methods: {
    toast,
    async postuser() {
      try {
        await AuthService.createsignup(this.usernew);
        this.toasts.title = "Success",
          this.toasts.msg = "Đăng ký thành công",
          this.toasts.type = "success",
          this.toasts.duration = 2000
        this.toast();
        setTimeout(() => {
          this.$router.push({ name: "login" });
        }, 2000);
      } catch (erorr) {
        console.log(erorr);
        this.toasts.title = "Faild",
          this.toasts.msg = "Thông tin bạn nhập đã được dùng",
          this.toasts.type = "error",
          this.toasts.duration = 2000
        this.toast();
      }
    }
  }
};
</script>

<template>
  <HeaderShop></HeaderShop>
  <toastsVue></toastsVue>
  <div style="padding: 20px 0 30px 0;">
    <div class="row signup-wrap" style="margin: auto;">
      <div class="signup-html">
        <h3 class="text-center text-white pb-2">ĐĂNG KÝ</h3>
        <div class="signup-form">
          <section class="">
            <div class="">
              <Form :validation-schema="Logupform">
                <div class="form-outline mb-4">
                  <label class="form-label label2 fw-bold" for="name">Tên tài khoản</label>
                  <Field placeholder="Nhập tên tài khoản" id="name" name="name" type="text" class="form-control"
                    v-model="usernew.username" />
                  <ErrorMessage name="name" class="label2" />
                </div>
                <div class="mb-4">
                  <label class="form-label label2 fw-bold" for="email">Email</label>
                  <div class="form-outline">
                    <Field placeholder="Nhập email" id="email" name="email" type="email" class="form-control"
                      v-model="usernew.email" />
                    <ErrorMessage name="email" class="label2" />
                  </div>
                </div>
                <div class="form-outline mb-4">
                  <label class="form-label label2 fw-bold" for="pwd">Mật khẩu</label>
                  <Field placeholder="Nhập mật khẩu" id="pwd" name="pwd" type="password" class="form-control"
                    v-model="usernew.password" />
                  <ErrorMessage name="pwd" class="label2" />
                </div>
                <div class="text-center t-lg-start mt-4 pt-2 ">
                  <button type="button" class="my-button" @click="postuser()">
                    Đăng Ký
                  </button>
                  <div class="hr"></div>
                  <p class="text-white">Bạn đã có tài khoản ? <router-link to="/login"
                      style="text-decoration: none; color: white; font-weight: bold;"> Đăng Nhập</router-link></p>
                </div>
              </Form>
            </div>
          </section>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped  >
.signup-wrap {
  width: 100%;
  margin: auto;
  max-width: 450px;
  min-height: 600px;
  position: relative;
  background: url(https://media.licdn.com/dms/image/D5612AQFoSspOIiDxiQ/article-cover_image-shrink_600_2000/0/1664099773634?e=2147483647&v=beta&t=1Tpxqag6iAcbsSyDI8redYKFp4UxqT8tnFGtXpiJiDs) no-repeat center;
  box-shadow: 0 12px 15px 0 rgba(0, 0, 0, .24), 0 17px 50px 0 rgba(0, 0, 0, .19);
}

.signup-html {
  width: 100%;
  height: 100%;
  position: absolute;
  padding-top: 40px;
  background: rgba(100, 109, 101, 0.577);
}

.hr {
  height: 2px;
  margin: 20px 0 30px 0;
  background: rgba(208, 207, 207, 0.2);
}

.form-control {
  width: 80%;
  margin-left: 10%;
}

.label2 {
  margin-left: 10%;
  color: white;
}
</style>
