<template>
  <div>
   <AdminHeader></AdminHeader>
    <div class="nav-welcome">
      <div class="background">
        <div class="tbox ">
          <div class="bod">
            <div class="pt-3">CHÀO MỪNG ĐẾN TRANG QUẢN TRỊ VIÊN</div>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <!-- Tab thông tin bên trên -->
      <div class="dashboard main-content">
        <a href="/listKH" class="admin-card-icon" style="text-decoration: none; color: black">
          <div class="admin-card-icon-body">
            <div class="admin-card-icon-i">
              <i class="fa fa-users"></i>
            </div>
            <h3>Người dùng</h3>
          </div>
        </a>
        <a href="/listSP" class="admin-card-icon" style="text-decoration: none; color: black">
          <div class="admin-card-icon-body">
            <div class="admin-card-icon-i">
              <i class="fa fa-shopping-bag"></i>
            </div>
            <h3>Sản phẩm</h3>
          </div>
        </a>
        <a href="/listDH" class="admin-card-icon" style="text-decoration: none; color: black">
          <div class="admin-card-icon-body">
            <div class="admin-card-icon-i">
              <i class="fa-solid fa-cart-shopping"></i>
            </div>
            <h3>Đơn hàng</h3>
          </div>
        </a>
        <!-- Top Sản phẩm -->
        <!-- <div class="table1">
          <div class="table-head">
            <h3 class="font-weight-bold mt-2">Top sản phẩm</h3>
          </div>
          <div class="table-body">
            <div class="table-responsive">
              <table>
                <thead>
                  <tr class="text-center">
                    <th>Tên sản phẩm</th>
                    <th>Giá bán</th>
                    <th>Giảm giá</th>
                    <th>Thao tác</th>
                  </tr>
                </thead>
                <tbody>
                  <TopTable v-for="(item, index) in products" :key="index" :product="item" />
                </tbody>
              </table>
            </div>
          </div>
        </div> -->

      </div>
    </div>
  </div>
</template>

<script>
import AdminHeader from "@/components/AdminHeader.vue";

export default {
  name: "Adminview",

  components: {
    AdminHeader,
  },
};
</script>

<style>
.nav-welcome {
  margin-left: 170px;
  z-index: -1;
  height: 120px;
}

.background {
  background-image: url(https://danangaz.com/wp-content/uploads/2020/03/cay-canh-hai-phong-2-min.jpg);
}

.tbox {
  font-size: 20px;
  text-align: center;
  color: white;
  padding: 40px;
  background-color: rgba(100, 109, 101, 0.7);
}

.bod {
  border: 2px solid white;
  height: 60px;
  font-weight: bold;
  width: 450px;
  margin-left: 390px;
  margin-bottom: 40px;
  
}

.main-content {
  padding: 20px 0 0 0;
  margin-left: 160px;
  z-index: -1;
  min-height: 600px;
}

.dashboard {
  display: flex;
  flex-wrap: wrap;
}

.admin-card-icon {
  flex: 1 1 18%;
  background: #ffffff;
  border-radius: 6px;
  border: 1px solid rgb(172, 227, 193);
  box-shadow: 0 3px 10px rgba(62, 85, 120, 0.045);
  margin: 0 8px 30px;
  height: 220px;
}

.admin-card-icon .admin-card-icon-body {
  padding: 40px;
}

.admin-card-icon-i {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  background-color: #e5f4e7;
  margin: 0 auto;
  position: relative;
}

.admin-card-icon .admin-card-icon-body h3 {
  text-align: center;
  margin-bottom: 0;
  margin-top: 10px;
  font-size: 18px;
  font-weight: 400;
}

.admin-card-icon-i i {
  top: 50%;
  text-align: center;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 45px;
  color: #5dae8b;
}

.btn-group {
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-group a {
  padding: 3px;
  width: 26px;
  height: 26px;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15) !important;
  margin: 0 5px;
  color: #fff;
  background-color: #5dae8b;
  border-color: #5dae8b;
  border-radius: 0.375rem;
  font-weight: 500;
}

.btn-group a {
  text-align: center;
  line-height: 25px;
  display: block;
}

@media only screen and (max-width: 768px) {
  .table {
    flex: 1 1 100%;
    overflow-x: scroll;
  }
}
</style>