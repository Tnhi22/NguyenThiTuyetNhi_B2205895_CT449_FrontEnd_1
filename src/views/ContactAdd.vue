<template>
  <div class="container page mt-3">
    <h4>Thêm Liên Hệ Mới</h4>
    <form @submit.prevent="saveContact">
      <div class="form-group mb-2">
        <label for="name">Tên:</label>
        <input v-model="contact.name" id="name" class="form-control" required />
      </div>

      <div class="form-group mb-2">
        <label for="email">Email:</label>
        <input
          v-model="contact.email"
          id="email"
          type="email"
          class="form-control"
        />
      </div>

      <div class="form-group mb-2">
        <label for="address">Địa chỉ:</label>
        <input v-model="contact.address" id="address" class="form-control" />
      </div>

      <div class="form-group mb-2">
        <label for="phone">Điện thoại:</label>
        <input v-model="contact.phone" id="phone" class="form-control" />
      </div>

      <div class="form-check mb-3">
        <input
          v-model="contact.favorite"
          id="favorite"
          type="checkbox"
          class="form-check-input"
        />
        <label for="favorite" class="form-check-label">Liên hệ yêu thích</label>
      </div>

      <div class="d-flex gap-2">
        <button type="submit" class="btn btn-success">
          <i class="fas fa-save"></i> Lưu
        </button>
        <button type="button" class="btn btn-secondary" @click="cancel">
          <i class="fas fa-arrow-left"></i> Quay lại
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import ContactService from "@/services/contact.service";

export default {
  data() {
    return {
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
    };
  },
  methods: {
    async saveContact() {
      try {
        await ContactService.create(this.contact);
        alert("Thêm liên hệ thành công!");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.error(error);
        alert("Có lỗi xảy ra khi thêm liên hệ!");
      }
    },
    cancel() {
      this.$router.push({ name: "contactbook" });
    },
  },
};
</script>

<style scoped>
.page {
  max-width: 600px;
  margin: auto;
}
</style>
