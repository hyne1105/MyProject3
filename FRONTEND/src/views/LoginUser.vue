<script>
import HeaderShop from "../components/HeaderShop.vue";
import FormloginVue from "../components/Formlogin.vue";
import toastsVue from "../components/toasts.vue";
export default {
  components: {
    HeaderShop,
    FormloginVue,
    toastsVue
  },
};
</script>
<template>
  <HeaderShop></HeaderShop>
  <toastsVue></toastsVue>
  <div style="padding: 20px 0 30px 0;">
    <div class="row login-wrap" style="margin: auto;">
      <div class="login-html">
        <h3 class="text-center text-white pb-2">ĐĂNG NHẬP</h3>
        <div class="login-form">
          <FormloginVue></FormloginVue>
        </div>
      </div>
    </div>
  </div>
</template>
<style></style>