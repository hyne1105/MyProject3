<template>
  <HeaderShop></HeaderShop>
  <div class="container pb-5">
    <h2 class="text-secondary text-center font-weight-bold m-4">
      VỀ CHÚNG TÔI
    </h2>
    <!-- About Start -->
    <div class="container-xxl">
      <div class="container pb-4">
        <div class="row g-5 align-items-end">
          <div class="col-lg-3 col-md-5 wow fadeInUp" data-wow-delay="0.1s">
            <img class="img-fluid rounded" data-wow-delay="0.1s" src="../assets/img/gioithieu.jpg">
          </div>
          <div class="col-lg-6 col-md-7 wow fadeInUp" data-wow-delay="0.3s">
            <h4 class="display-4 mb-0 color">24/7</h4>
            <p class="color mb-4 ">Luôn sẵn sàng phục vụ cho nhu cầu mua cây xanh của bạn</p>
            <h1 class="display-5 mb-4 text-muted">MANG ĐẾN CHO BẠN MÀU XANH TƯƠI ĐẸP</h1>
            <p class="mb-4">GREEN cung cấp các loại Cây cảnh để bàn, Sen Đá, Xương Rồng & Tiểu cảnh Terrarium trang trí
              nội thất, văn phòng.</p>
            <p class="mb-4">Chúng tôi luôn cố gắng tạo ra những sản phẩm đẹp, khác biệt hoàn toàn so với thị trường để đáp
              ứng mọi nhu cầu của khách hàng với mẫu mã đa dạng, phong phú.</p>
            <button class="btton">Khám phá ngay</button>
          </div>
          <div class="col-lg-3 col-md-12 wow fadeInUp" data-wow-delay="0.5s">
            <div class="row g-5">
              <div class="col-12 col-sm-6 col-lg-12">
                <div class="border-start ps-4">
                  <i class="fa fa-thumbs-up fa-3x mb-3 color"></i>
                  <h4 class="mb-3">Cam Kết Chất Lượng</h4>
                  <span class="text-muted">Chúng tôi luôn muốn mang đến cho khách hàng những sản phẩm chất lượng tốt nhất.</span>
                </div>
              </div>
              <div class="col-12 col-sm-6 col-lg-12">
                <div class="border-start ps-4">
                  <i class="fa fa-users fa-3x mb-3 color"></i>
                  <h4 class="mb-3">Làm Việc Tận Tình</h4>
                  <span class="text-muted">Hãy liên hệ ngay nếu bạn có thắc mắc hoặc cần tư vấn. Chúng tôi luôn sẵn sàng phục vụ.</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- About End -->
  </div>
  <FooterShop></FooterShop>
</template>

<script>
import HeaderShop from '@/components/HeaderShop.vue';
import FooterShop from '@/components/FooterShop.vue'

export default{
  components: {
    HeaderShop,
    FooterShop,
  }
}
</script>

<style></style>
