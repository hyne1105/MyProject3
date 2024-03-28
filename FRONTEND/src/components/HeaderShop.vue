<script>
import CartService from '../services/Cart.service';
import { mapState, mapActions } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
import toast from '../assets/js/toasts';

export default {
  data() {
    return {
      carts: [],
      toasts: {
        title: "Warning",
        msg: "Bạn chưa đăng nhập",
        type: "warn",
        duration: 3000
      },
    }
  },
  computed: {
    ...mapState(useAuthStore, {
      currentUser: "user",
    }),
    getlengthcarts() {
      return this.carts.length;
    },
  },
  methods: {
    toast,
    ...mapActions(useAuthStore, ["logout", "loadAuthState"]),
    slideSearch: function () {
      this.$el.querySelector("#input_search").classList.toggle("input_search");
      this.$el.querySelector("#input_search").focus();
    },
    async showcarts() {
      try {
        this.showuser();
        if (this.currentUser != null) {
          this.carts = await CartService.get(this.currentUser._id);
        }
      } catch (error) {
        console.log(error);
      }
    },
    showuser() {
      if (this.currentUser == null) {
        document.querySelector('.login').style.display = "none";
        document.querySelector('.not-login').style.display = "block";
      } else {
        document.querySelector('.login').style.display = "block";
        document.querySelector('.not-login').style.display = "none";
        document.querySelector('.data_user').innerHTML = this.currentUser.username;
      }
    },
    handlelogout() {
      this.logout();
      this.$router.push({ name: "login" });
    },
    gotocart() {
      if (!this.currentUser) {
        this.toast();
      } else {
        this.$router.push({ name: "CartShop" });
      }
    }
  },
  created() {
    this.loadAuthState();
  },
  mounted() {
    this.showcarts();
  },
};
</script>

<template>
  <!-- Topbar Start -->
  <div class="topbar container-fluid text-light">
    <div class="topbar container">
      <div class="row">
        <div class="col-7">
          <div class="h-100 d-inline-flex align-items-center me-4">
            <span class="fa fa-phone-alt me-2"></span>
            <span>0946053795</span>
          </div>
          <div class="h-100 d-inline-flex align-items-center">
            <span class="far fa-envelope me-2"></span>
            <span>greenshop@gmail.com</span>
          </div>
        </div>
        <div class="col-5 text-end">
          <div class="align-items-center">
            <span>Kết nối với chúng tôi:</span>
            <a class="btn btn-link text-light" href=""><i class="fab fa-facebook-f"></i></a>
            <a class="btn btn-link text-light" href=""><i class="fab fa-instagram"></i></a>
            <a class="btn btn-link text-light" href=""><i class="fab fa-twitter"></i></a>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Topbar End -->


  <nav class="navbar navbar-expand">
    <div class="container">
      <div>
        <img src="../assets/img/green-high-resolution-logo.png" style="width: 200px;">
      </div>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto">
          <li class="nav-item mx-3">
            <router-link to="/" class="nav-link text-success" aria-current="page">
              TRANG CHỦ
            </router-link>
          </li>
          <li class="nav-item mx-3">
            <router-link to="/about" class="nav-link" style="text-decoration: none">
              GIỚI THIỆU
            </router-link>
          </li>
          <li class="nav-item mx-3">
            <router-link to="/contact" class="nav-link" style="text-decoration: none">
              LIÊN HỆ
            </router-link>
          </li>
        </ul>
        
        <div class="Cart">
          <div class="wrapper_cart">
            <div class="cart_link" id="cart_link">
              <div>
                <div>
                  <router-link to="/cart" style="text-decoration: none;"></router-link>
                </div>
              </div>
            </div>
            <i class="bi bi bi-cart3 icon " @click="gotocart" style="color: #00b214;"></i>
          </div>
        </div>

        <div class="User">
          <div class="not-login">
            <i class="bi bi-person-circle icon" data-bs-toggle="collapse" href="#user"></i>
            <div class="collapse user_link" id="user">
              <div class="card card-body bg-light connect-shop">
                <router-link to="/login" class="text-black">Đăng nhập</router-link>
                <router-link to="/logup" class="text-black">Đăng ký</router-link>
              </div>
            </div>
          </div>
          <div>
            <span class="text-light data_user" data-bs-toggle="collapse" href="#user"></span>
            <div class="collapse user_link" id="user">
              <div class="card card-body bg-light connect-shop">
                <router-link to="/profile" class="text-black">Trang cá nhân</router-link>
                <a to="/" class="text-black" @click="handlelogout()">Đăng nhập</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar-nav {
  text-align: center;
  font-size: 18px;
  font-weight: 600;
}

.navbar {
  height: 80px;
  background-color: white;
}

.topbar {
  background-color: #00b214;
}

.container-fluid {
  background-image: url('../assets/img/bg1.jpg');
}

.connect-shop {
  padding: 0px
}

.connect-shop a:hover {
  background-color: rgb(187, 187, 187);
}

.connect-shop a {
  padding: 10px 10px;
}

.User,
.Cart {
  margin-left: 10px;
}

.wrapper_cart {
  position: relative;
  width: 50px;
  height: 50px;
}

.cart_link {
  position: absolute;
  top: 100%;
  right: 0;
  width: 500px;
  display: none;
  z-index: 100;
  overflow-y: scroll;
  max-height: 500px;
}

#cart_link::-webkit-scrollbar {
  width: 6px;
  background-color: #F5F5F5;
}

.wrapper_cart:hover>.cart_link {
  cursor: pointer;
  display: block;
  animation: fadeIn .8s ease;
}

.user_link {
  width: 200px;
  text-align: end;
  position: absolute;
  top: 97%;
  right: 90px;
  z-index: 10;
}

.user_link a {
  display: block;
  text-decoration: none;
}

@keyframes Search {
  0% {
    transform: translateX(5%);
  }

  100% {
    transform: translateX(0%);
  }
}

</style>