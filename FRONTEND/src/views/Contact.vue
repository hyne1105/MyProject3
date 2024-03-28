<template>
  <HeaderShop></HeaderShop>
  <div class="container mt-4 pb-5">
    <h2 class="text-secondary text-center font-weight-bold mb-4">
      LIÊN HỆ
    </h2>
    <div class="row">
      <!-- Contact Start -->
      <div class="container-xxl py-3">
        <div class="container">
          <div class="row g-5">
            <div class="col-lg-6">
              <h2 class="fs-4 fw-bold color">Liên Hệ Chúng Tôi</h2>
              <h4 class="mb-3 text-muted">Nếu có bất cứ câu hỏi nào, vui lòng liên hệ chúng tôi</h4>
              <form>
                <div class="row g-3">
                  <div class="col-md-6">
                    <div class="form-floating">
                      <input type="text" class="form-control" id="name" placeholder="Nhập tên">
                      <label for="name">Tên của bạn</label>
                    </div>
                  </div>
                  <div class="col-md-6">
                    <div class="form-floating">
                      <input type="email" class="form-control" id="email" placeholder="Nhập email">
                      <label for="email">Email của bạn</label>
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="form-floating">
                      <input type="text" class="form-control" id="phonenumber" placeholder="Nhập số điện thoại">
                      <label for="phonenumber">Số điện thoại</label>
                    </div>
                  </div>
                  <div class="col-12">
                    <div class="form-floating">
                      <textarea class="form-control" placeholder="Nhập lời nhắn" id="message"
                        style="height: 100px"></textarea>
                      <label for="message">Lời nhắn</label>
                    </div>
                  </div>
                  <div class="col-12 pt-3">
                    <button class="btton" type="submit">
                      Gửi
                    </button>
                  </div>
                </div>
              </form>
            </div>
            <div class="col-lg-6 wow fadeIn" data-wow-delay="0.5s" style="min-height: 450px;">
              <div class="position-relative rounded overflow-hidden h-100">
                <iframe
                  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d62860.40232482591!2d105.71439047236652!3d10.035404978504333!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x31a0883fbc944b83%3A0x77fc34233e5e1320!2zTmluaCBLaeG7gXUsIEPhuqduIFRoxqEsIFZp4buHdCBOYW0!5e0!3m2!1svi!2s!4v1699340886821!5m2!1svi!2s"
                  class="position-relative w-100 h-100"></iframe>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Contact End -->
    </div>
  </div>
  <FooterShop></FooterShop>
</template>

<script>
import HeaderShop from '@/components/HeaderShop.vue';
import FooterShop from '@/components/FooterShop.vue'

export default {
  components: {
    HeaderShop,
    FooterShop,
  }
};
</script>

<style></style>
