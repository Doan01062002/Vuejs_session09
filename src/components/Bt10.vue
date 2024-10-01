<template>
  <div class="container">
    <form @submit.prevent="addUser">
      <div class="form-group">
        <label for="userEmail">Email</label>
        <input
          type="text"
          class="form-control"
          id="userEmail"
          v-model="user.email"
        />
      </div>
      <div class="form-group">
        <label for="userPassword">Mật khẩu</label>
        <input
          type="password"
          class="form-control"
          id="userPassword"
          v-model="user.password"
        />
      </div>

      <button type="submit" class="btn btn-custom btn-block">Đăng nhập</button>
    </form>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const user = reactive({
  id: Math.floor(Math.random() * 100000),
  name: "",
  email: "",
  password: "",
  phone: "",
});

// Lấy dữ liệu từ localStorage và kiểm tra kiểu dữ liệu
let users;
try {
  users = JSON.parse(localStorage.getItem("users")) || [];
  if (!Array.isArray(users)) {
    users = [];
  }
} catch (error) {
  users = [];
}

const addUser = () => {
  const checkEmail = users.find((item) => item.email === user.email);
  const checkPassword = users.find((item) => item.password === user.password);

  if (!checkEmail || !checkPassword) {
    alert("Thông tin tài khoản không chính xác");
  } else {
    alert("Đăng nhập thành công");
  }
};
</script>

<style scoped>
.container {
  max-width: 400px;
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.btn-custom {
  background-color: #007bff;
  color: white;
}
</style>
