<template>
  <div class="container">
    <form @submit.prevent="addUser">
      <div class="form-group">
        <label for="userName">Tên sinh viên</label>
        <input
          type="text"
          class="form-control"
          id="userName"
          v-model="user.name"
        />
      </div>
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
      <div class="form-group">
        <label for="userPhone">Số điện thoại</label>
        <input class="form-control" id="userPhone" v-model="user.phone" />
      </div>
      <button type="submit" class="btn btn-custom btn-block">Đăng ký</button>
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

  if (!user.name || !user.email || !user.password || !user.phone) {
    alert("Thông tin tài khoản không được để trống");
  } else if (checkEmail) {
    alert("Email đã tồn tại");
  } else {
    users.push({ ...user });
    localStorage.setItem("users", JSON.stringify(users));
    alert("Đăng ký thành công");
    resetForm();
  }
};

const resetForm = () => {
  user.name = "";
  user.email = "";
  user.password = "";
  user.phone = "";
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
