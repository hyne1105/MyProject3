<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
export default {
  props: {
    product: { type: Object, required: true },
    resetAfterSubmit: { type: Boolean, default: false },
  }
  ,
  data() {
    const productform = yup.object().shape({
      name: yup
        .string()
        .required("Tên phải có giá trị.")
        .min(5, "Tên phải ít nhất 5 ký tự."),
      img: yup
        .string()
        .required("Hình ảnh phải có giá trị."),
      price: yup
        .string()
        .required("Giá sản phẩm phải có giá trị."),
      description: yup
        .string()
        .required("Mô tả sản phẩm phải có giá trị.")
        .min(5, "Tên phải ít nhất 5 ký tự."),
      category: yup
        .string()
        .required("Loại sản phẩm phải có giá trị."),
      size: yup
        .string()
        .required("Kích thước sản phẩm phải có giá trị."),
      color: yup
        .string()
        .required("Màu sắc sản phẩm phải có giá trị."),
    });
    return {
      productLocal: this.product,
      productform,
    }
  },
  components: {
    Form,
    Field,
    ErrorMessage
  },
  emits: ['submit:product'],
  methods: {
    addImge() {
      document.querySelector("#imgproduct2").style.display = "block";
    },
    submitproduct() {
      this.$emit('submit:product', this.productLocal);
      if (this.resetAfterSubmit) {
        this.$refs.contactForm.resetForm();
      }
    },
  }
}
</script>
<template>
  <div style="padding: 30px 0 30px 235px">
    <Form class="card2" :validation-schema="productform" @submit="submitproduct">
      <div class="card2-header">
        <div class="text-header">BẢNG SẢN PHẨM</div>
      </div>
      <div class="card2-body">
          <div class="form-group2">
            <label for="nameproduct">TÊN SẢN PHẨM</label>
            <Field type="text" class="form-control" id="nameproduct" name="name" v-model="productLocal.title" />
            <ErrorMessage name="name" class="text-danger" />
          </div>
          <div class="form-group2">
            <label for="imgproduct">HÌNH ẢNH</label>
            <div style="display: flex; flex-direction: row;">
              <Field type="text" class="form-control" id="imgproduct" name="img" v-model="productLocal.img[0]" />
              <i class="bi bi-file-plus btn_img-add" @click="addImge()"></i>
            </div>
            <input type="text" class="form-control" id="imgproduct2" name="img" style="display:none; margin: 10px 0;"
              v-model="productLocal.img[1]">
            <ErrorMessage name="img" class="text-danger" />
          </div>
          <div class="form-group2">
            <label for="priceproduct">GIÁ</label>
            <Field type="number" class="form-control" id="priceproduct" name="price" v-model="productLocal.price" />
            <ErrorMessage name="price" class="text-danger" />
          </div>
          <div class="form-group2">
            <label for="nameproduct">MÔ TẢ</label>
            <Field type="text" class="form-control" id="nameproduct" name="description" v-model="productLocal.desc" />
            <ErrorMessage name="description" class="text-danger" />
          </div>
          <div class="form-group2">
            <label for="categoryproduct">LOẠI CÂY</label>
            <Field type="text" class="form-control" id="categoryproduct" name="category"
              v-model="productLocal.categories" />
            <ErrorMessage name="category" class="text-danger" />
          </div>
          <div class="form-group2">
            <label for="sizeproduct">KÍCH THƯỚC</label>
            <Field type="text" class="form-control" id="sizeproduct" name="size" v-model="productLocal.size" />
            <ErrorMessage name="size" class="text-danger" />
          </div>
          <div class="form-group2">
            <label for="colorproduct">MÀU CHẬU</label>
            <Field type="text" class="form-control" id="colorproduct" name="color" v-model="productLocal.color" />
            <ErrorMessage name="color" class="text-danger" />
          </div>
          <div class="row pt-4">
            <router-link to="/ListSP" class="col-6">
              <button class="btn btn-danger">Trở về</button>
            </router-link>
            <div class="col-6 d-flex justify-content-end">
              <button type="submit" class="btn2">Lưu</button>
            </div>
          </div>
      </div>
    </Form>
  </div>
</template>
<style scoped>
.wrapper {
  margin: 50px 200px;
}

.btn_img-add {
  font-size: 30px;
  color: rgb(0, 0, 0);
}

.card2 {
  width: 1200px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin: 10px;
}

.card2-header {
  background-color: #333;
  padding: 16px;
  text-align: center;
}

.card2-header .text-header {
  margin: 0;
  font-size: 18px;
  color: rgb(255, 255, 255);
}

.card2-body {
  padding: 16px;
}

.form-group2 {
  margin-bottom: 10px;
}

.form-group2 label {
  display: block;
  font-size: 14px;
  color: #333;
  font-weight: bold;
  margin-bottom: 1px;
}

.form-group2 input[type="text"],
.form-group2 input[type="email"],
.form-group2 input[type="password"] {
  width: 100%;
  padding: 8px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.btn2 {
  padding: 10px 20px;
  margin-left: 13px;
  font-size: 14px;
  border: none;
  border-radius: 4px;
  background-color: #333;
  color: #fff;
  text-transform: uppercase;
  transition: background-color 0.2s ease-in-out;
  cursor: pointer
}

.btn2:hover {
  background-color: #ccc;
  color: #333;
}
</style>