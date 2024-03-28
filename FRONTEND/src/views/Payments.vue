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
    <h3 style="text-align: center; padding-top: 30px;">XÁC NHẬN THANH TOÁN</h3>
    <div class="row">
      <div class="col-8">
        <div class="prod">
          <div>
            <h6 class="mb-0 text-muted">{{ carts.length }} sản phẩm</h6>
          </div>
          <hr class="my-4">
          <CartItem :refeshlistcart="refeshlistcart" :carts="carts" @deleted:cartIndex="delcart"></CartItem>
          <div class="row">
            <div class="col-8">
              <router-link to="/cart">
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
            <div class="col-md-6 payments">
              <span>Thanh toán trực tuyến</span>
              <div class="card">
                <div class="accordion" id="accordionExample">
                  <div class="card">
                    <div class="card-header p-0" id="headingTwo">
                      <h2 class="mb-0">
                        <button class="btn btn-light btn-block text-left collapsed p-3 rounded-0 border-bottom-custom"
                          type="button" data-toggle="collapse" data-target="#collapseTwo" aria-expanded="false"
                          aria-controls="collapseTwo">
                          <div class="d-flex align-items-center justify-content-between">
                            <span class="me-2">Paypal</span>
                            <img src="https://i.imgur.com/7kQEsHU.png" width="30">
                          </div>
                        </button>
                      </h2>
                    </div>
                    <div id="collapseTwo" class="collapse" aria-labelledby="headingTwo" data-parent="#accordionExample">
                      <div class="card-body">
                        <input type="text" class="form-control" placeholder="Paypal email">
                      </div>
                    </div>
                  </div>

                  <div class="card">
                    <div class="card-header p-0">
                      <h2 class="mb-0">
                        <button class="btn btn-light btn-block text-left p-3 rounded-0" data-toggle="collapse"
                          data-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                          <div class="d-flex align-items-center justify-content-between">
                            <span class="me-2">Loại thẻ: </span>
                            <div class="icons">
                              <img src="https://i.imgur.com/2ISgYja.png" width="30">
                              <img src="https://i.imgur.com/W1vtnOV.png" width="30">
                              <img src="https://i.imgur.com/35tC99g.png" width="30">
                              <img src="https://i.imgur.com/2ISgYja.png" width="30">
                            </div>
                          </div>
                        </button>
                      </h2>
                    </div>

                    <div id="collapseOne" class="collapse show" aria-labelledby="headingOne"
                      data-parent="#accordionExample">
                      <div class="card-body payment-card-body">
                        <span class="font-weight-normal card-text">Số thẻ</span>
                        <div class="input">
                          <i class="fa fa-credit-card"></i>
                          <input type="text" class="form-control" placeholder="0000 0000 0000 0000">
                        </div>
                        <div class="row mt-3 mb-3">
                          <div class="col-md-6">
                            <span class="font-weight-normal card-text">Ngày </span>
                            <div class="input">
                              <i class="fa fa-calendar"></i>
                              <input type="text" class="form-control" placeholder="MM/YY">
                            </div>
                          </div>
                          <div class="col-md-6">
                            <span class="font-weight-normal card-text">CVC/CVV</span>
                            <div class="input">
                              <i class="fa fa-lock"></i>
                              <input type="text" class="form-control" placeholder="000">
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="my-5 container d-flex justify-content-center">
          <button class="button3" @click="handelbuttonaddorder()">
            <router-link to="/thank" class="text-white" style="text-decoration: none;">Thanh Toán</router-link>
          </button>
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

.total {}

.btn3 {}

@media (min-width: 1025px) {
  .h-custom {
    height: 100%;
  }
}

.card-registration .select-input.form-control[readonly]:not([disabled]) {
  font-size: 1rem;
  line-height: 2.15;
  padding-left: .75em;
  padding-right: .75em;
}

.card-registration .select-arrow {
  top: 13px;
}

.bg-grey {
  background-color: #ffffff;
}

@media (min-width: 992px) {
  .card-registration-2 .bg-grey {
    border-top-right-radius: 16px;
    border-bottom-right-radius: 16px;
  }
}

@media (max-width: 991px) {
  .card-registration-2 .bg-grey {
    border-bottom-left-radius: 16px;
    border-bottom-right-radius: 16px;
  }
}
</style>