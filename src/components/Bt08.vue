<template>
  <div class="container">
    <form @submit.prevent="addUser">
      <div class="form-group">
        <label for="userCode">Họ và tên</label>
        <input
          type="text"
          class="form-control"
          id="userCode"
          v-model="user.name"
          required
        />
      </div>
      <div class="form-group">
        <label for="userCode">Email</label>
        <input
          type="text"
          class="form-control"
          id="userCode"
          v-model="user.email"
          required
        />
      </div>
      <div class="form-group">
        <label for="userCode">Mật khẩu</label>
        <input
          type="text"
          class="form-control"
          id="userCode"
          v-model="user.password"
          required
        />
      </div>
      <div class="form-group">
        <label for="userCode">Nhập lại mật khẩu</label>
        <input
          class="form-control"
          id="userCode"
          v-model="user.rePassword"
        >
        </input>
      </div>
      <button type="submit" class="btn btn-custom btn-block">Thêm mới</button>
    </form>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const user = reactive({
    id: Math.floor(Math.random()*100000),
  name: "",
  email: "",
  password: "",
  rePassword: "",
});

const addUser = () => {
  console.log("User mới:", user);
};
</script>

<style scoped>
.container {
  max-width: 400px;
  margin-top: 50px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.btn-custom {
  background-color: #007bff;
  color: white;
}
</style>
