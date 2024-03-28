<script>
import { mapState } from "pinia";
import { useAuthStore } from "../stores/Auth.store";
import HeaderShop from '@/components/HeaderShop.vue';
import FooterShop from '@/components/FooterShop.vue';
import CartService from '../services/Cart.service';
import toastsVue from '../components/toasts.vue';
import toastsjs from '../assets/js/toasts.js'
import CartItem from "../components/CartItem.vue";
import OrderService from '../services/Order.service';
export default {
  data() {
    return {
      carts: [],
      toasts: {
        title: "",
        msg: "",
        type: "",
        duration: 0
      },
    }
  },
  components: {
    HeaderShop,
    toastsVue,
    CartItem,
    FooterShop,
  },
  computed: {
    ...mapState(useAuthStore, {
      currentUser: "user",
    }),
  },
  methods: {
    getiduser() {
      const user = JSON.parse(localStorage.getItem("user"));
      return user._id;
    },
    async handelbuttonaddorder() {
      for (let item of this.carts) {
        let order = {
          userId: item.userId,
          productId: item._id,
          quantity: item.quantity,
          address: "Lấy tại shop",
          status: "Chờ xác nhận",
        };
        await OrderService.create(order);
      }
    },
    async getcarts() {
      try {
        this.carts = await CartService.get(this.getiduser());
      } catch (error) {
        console.log(error);
      }
    },
    async delcart(index) {
      // this.toasts.title = "Deleted",
      // this.toasts.msg = "XÓA SẢN PHẨM THÀNH CÔNG",
      // this.toasts.type = "error",
      // this.toasts.duration = 2000
      // this.toastsjs();
      await CartService.delete(this.carts[index]._id)
      this.refeshlistcart();
    },
    toastsjs,
    refeshlistcart() {
      this.getcarts();
    },
    registerproduct() {
      if (this.carts.length > 0) {

        this.toasts.msg = "THANH TOÁN THÀNH CÔNG",
          this.toasts.type = "success",
          this.toasts.duration = 2000,
          this.toastsjs();
      } else {
        this.toasts.title = "Failed",
          this.toasts.msg = "Bạn chưa có sản phẩm",
          this.toasts.type = "error",
          this.toasts.duration = 2000,
          this.toastsjs();
      }
    },
    total() {
      var total = 0;
      for (var i in this.carts) {
        total += (this.carts[i].price * this.carts[i].quantity);
      }
      return total;
    }
  },
  created() {
    this.refeshlistcart();
  },
}
</script>

<template>
  <HeaderShop></HeaderShop>
  <toastsVue></toastsVue>
  <div class="container cart shadow-sm p-3 mb-5 bg-body rounded">
    <h3 style="text-align: center; padding-top: 30px;">GIỎ HÀNG</h3>
    <div class="row" style="justify-content: flex-start">
      <div class="col-8">
        <div class="prod">
          <div>
            <h6 class="mb-0 text-muted">{{ carts.length }} sản phẩm</h6>
          </div>
          <hr class="my-4">
          <CartItem :refeshlistcart="refeshlistcart" :carts="carts" @deleted:cartIndex="delcart"></CartItem>
          <div class="row">
            <div class="col-8">
              <router-link to="/">
                <button class="button2">
                  <div class="button-box">
                    <span class="button-elem">
                      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 46 40">
                        <path
                          d="M46 20.038c0-.7-.3-1.5-.8-2.1l-16-17c-1.1-1-3.2-1.4-4.4-.3-1.2 1.1-1.2 3.3 0 4.4l11.3 11.9H3c-1.7 0-3 1.3-3 3s1.3 3 3 3h33.1l-11.3 11.9c-1 1-1.2 3.3 0 4.4 1.2 1.1 3.3.8 4.4-.3l16-17c.5-.5.8-1.1.8-1.9z">
                        </path>
                      </svg>
                    </span>
                    <span class="button-elem">
                      <svg viewBox="0 0 46 40">
                        <path
                          d="M46 20.038c0-.7-.3-1.5-.8-2.1l-16-17c-1.1-1-3.2-1.4-4.4-.3-1.2 1.1-1.2 3.3 0 4.4l11.3 11.9H3c-1.7 0-3 1.3-3 3s1.3 3 3 3h33.1l-11.3 11.9c-1 1-1.2 3.3 0 4.4 1.2 1.1 3.3.8 4.4-.3l16-17c.5-.5.8-1.1.8-1.9z">
                        </path>
                      </svg>
                    </span>
                  </div>
                </button>
              </router-link>
            </div>
            <div class="col-4 total text-end">
              <h5 class="pt-3 mb-5">TỔNG TIỀN: {{ total().toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} VNĐ</h5>
            </div>
          </div>

        </div>
      </div>
      <div class="col-4">
        <div class="container">
          <div class="row g-3">
            <div class="col-md-6 payments pt-5">
              <div class="bill">
                <h4 class="text-center pt-4">ĐƠN HÀNG</h4>
                <div class="text-center py-3">
                  <span>Giá: {{ total().toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
                  }} VNĐ</span>
                  <br />
                  <span>Số lượng sản phẩm: {{ carts.length }}</span>
                  <br />
                  <span>Vận chuyển: Miễn phí</span>
                </div>
                <hr>
                <div>
                  <div class="text-center fw-bold pt-2">
                    <span>TỔNG TIỀN: {{ total().toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} VNĐ</span>
                  </div>
                  <div class="my-4 container d-flex justify-content-center">
                    <button class="button3">
                      <router-link to="/payments" class="text-white" style="text-decoration: none;">Xác Nhận Đơn
                        Hàng</router-link>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <FooterShop></FooterShop>
</template>
<style scoped>
.cart {
  background-color: white;
  margin: 30px auto;
  min-height: 600px;
}

.prod {
  padding-left: 40px;
}

.payments {
  width: 360px;
  margin: auto;
}

.bill{
  border: 1px solid #00b201;
  border-radius: 10px;
}

.total {}
</style>