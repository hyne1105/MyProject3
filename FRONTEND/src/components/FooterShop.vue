<template >
 <!-- Footer Start -->
 <div class="bagr footer">
    <div class="bagr container">
      <div class="row pt-4">
        <div class="col-lg-3 col-md-6">
          <div class="footer-item">
            <h1 class="text-footer">GREEN</h1>
            <p class="lh-lg mb-4 text-muted">Chúng tôi muốn biến tất những chậu cây cảnh thành những tác phẩm nghệ thuật
              với tất cả niềm đam mê và tâm huyết của mình.</p>
            <div class="footer-icon d-flex">
              <a class="btn btn-footer btn-sm-square me-2 rounded-circle" href=""><i class="fab fa-facebook-f"></i></a>
              <a class="btn btn-footer btn-sm-square me-2 rounded-circle" href=""><i class="fab fa-twitter"></i></a>
              <a href="#" class="btn btn-footer btn-sm-square me-2 rounded-circle"><i class="fab fa-instagram"></i></a>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 ">
          <div class="footer-item">
            <h4 class="mb-4 fw-bold text-muted">Đường dẫn nhanh</h4>
            <div class="d-flex flex-column align-items-start">
              <a class="text-body text-muted mb-3" href="/about"><i class="fa fa-check text-footer me-2"></i>Giới thiệu</a>
              <a class="text-body text-muted mb-3" href="/contact"><i class="fa fa-check text-footer me-2"></i>Liên hệ</a>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-md-6 text-muted">
          <div class="footer-item">
            <h4 class="mb-4 fw-bold">Liên hệ chúng tôi</h4>
            <div class="d-flex flex-column align-items-start">
              <p><i class="fa fa-map-marker-alt text-footer me-2"></i>Ninh Kiều, Cần Thơ</p>
              <p><i class="fa fa-phone-alt text-footer me-2"></i> 0946053795</p>
              <p><i class="fas fa-envelope text-footer me-2"></i> greenshop@gmail.com</p>
              <p><i class="fa fa-clock text-footer me-2"></i>Dịch vụ 24/7</p>
            </div>
          </div>
        </div>
        <div class="col-lg-3 col-md-6">
          <div class="footer-section">
            <div class="tree-img">
              <img src="../assets/img/footer.png" alt="image" class="img-fluid">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Footer End -->


  <!-- Copyright Start -->
  <div class="container-fluid copyright btn-footer py-2">
    <div class="container">
      <div class="row text-center">
          <a href="#" class="text-white">Copyright <i class="fas fa-copyright text-light me-2"></i>2023.</a>
      </div>
    </div>
  </div>
  <!-- Copyright End -->
</template>
<style scoped>
a {
  color: black;
  text-decoration: none;
}

.footer .footer-item a.text-body:hover {
  color: var(--bs-success) !important;
}

.text-footer {
  color: #00b214;
}

.btn-footer {
  background-color: #00b214;
  color: white;
}

.footer-section {
  height: 270px;
}

.footer-section .tree-img {
  position: relative;
  top: -100px;
  z-index: 1;
  right: 0;
}

.footer-section .tree-img img {
  max-width: 400px;
}

</style>