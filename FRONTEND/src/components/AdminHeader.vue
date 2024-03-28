<script>
import ListUser from "../components/ListUser.vue";
import UserService from "../services/User.service";
import ProductService from "../services/Product.service";
import ListProduct from "../components/ListProduct.vue";
import Productcard from "../components/Productcard.vue";
import Usercard from "../components/Usercard.vue";
import toast from "../assets/js/toasts";;
export default {
  data() {
    return {
      users: [],
      products: [],
      activeIndex: -1,
      activeUser: -1,
      toasts: {
        title: "Warning",
        msg: "Bạn không phải ADMIN",
        type: "warn",
        duration: 3000
      },
    }
  },
  computed: {
    getindex() {
      if (this.activeIndex != -1) {
        const list = document.querySelectorAll(".product-item");
        list.forEach(element => {
          element.classList.remove("active");
        });
        list[this.activeIndex].classList.add("active");
        return this.products[this.activeIndex];
      }
    },
    getindexuser() {
      if (this.activeUser != -1) {
        const list = document.querySelectorAll(".user-item");
        list.forEach(element => {
          element.classList.remove("active");
        });
        list[this.activeUser].classList.add("active");
        return this.users[this.activeUser];
      }
    }
  },
  components: {
    ListUser,
    ListProduct,
    Productcard,
    Usercard
  },
  methods: {
    toast,
    async getall() {
      try {
        this.products = await ProductService.getAll();
        this.users = await UserService.getAll();
      } catch (error) {
        console.log(error);
        this.toast();
        setTimeout(() => {
          this.$router.push({ name: "ShopMain" });
        }, 1000);
      }
    },
  },
  created() {
    this.getall();
  },
}
</script>

<template>
  <div class="nav">
    <div class="sidebar-list" id="sidebar">
      <div class="sidebar-list-item">
        <router-link style="text-decoration: none" :to="{ name: 'admin' }">
          <i class="fa fa-home pt-2">
            <div class="textnav">Tổng quan</div>
          </i>
        </router-link>
      </div>
      <div class="sidebar-list-item">
        <router-link style="text-decoration: none" :to="{ name: 'ListUser' }">
          <i class="fa fa-user pt-2">
            <div class="textnav">Người dùng</div>
          </i>
        </router-link>
      </div>
      <div class="sidebar-list-item">
        <router-link style="text-decoration: none" :to="{ name: 'ListProduct' }">
          <i class="fa fa-shopping-bag pt-2">
            <div class="textnav">Sản phẩm</div>
          </i>
        </router-link>
      </div>
      <div class="sidebar-list-item">
          <router-link style="text-decoration: none" :to="{ name: 'ListOrder' }">
            <i class="fa fa-shopping-cart pt-2">
              <div class="textnav"> Đơn hàng</div>
            </i>
          </router-link>
        </div>
      <div class="sidebar-list-item">
        <a href="/" style="text-decoration: none">
        <i class="fa fa-sign-out pt-2">
          <div class="textnav">Thoát</div>
        </i>
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.nav {
  width: 170px;
  height: 100%;
  background-color: #000000;
  display: inline-block;
  z-index: 5;
  position: fixed;
}


.sidebar-list {
  position: fixed;
  top: 30px;
  z-index: 5;
  display: flex;
  flex-direction: column;
  width: 170px;

}

.sidebar-list-item {
  flex: 1;
  margin: 25px 0;
  position: relative;
  text-align: center;
}

.sidebar-list-item i {
  color: white;
  font-size: 18px;
  display: block;
  line-height: 1;
}

.sidebar-list-item :hover {
  background-color: rgb(57, 151, 107);
  text-align: center;
}

.textnav {
  color: white;
  height: 40px;
  padding-top: 10px;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}

.show {
  display: block !important;
}
</style>