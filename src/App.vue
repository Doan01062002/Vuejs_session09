<!-- <template>
  <div>
    <p>One-way binding</p>
    <p>Hiển thị giá trị count: {{ count }}</p>
    <button @click="handleClick">click</button>
    <br />
    <br />
    <OneWayData></OneWayData>
    <br />
    <p>Two way data</p>
    <TwoWayData></TwoWayData>
  </div>
</template>
<script setup>
import { ref } from "vue";
import OneWayData from "./components/OneWayData.vue";
import TwoWayData from "./components/TwoWayData.vue";

const count = ref(0);
const handleClick = () => {
  count.value++;
};
</script>
<style></style> -->

<template>
  <div>
    <Bt01></Bt01>
    <Bt02></Bt02>
    <Bt03></Bt03>
    <Bt04></Bt04>
    <Bt05></Bt05>
    <Bt06></Bt06>
    <h3>Thêm mới sản phẩm</h3>
    <Bt07></Bt07>
    <h3>Thêm mới tài khoản</h3>
    <Bt08></Bt08>
    <h3>Đăng ký tài khoản</h3>
    <Bt09></Bt09>
    <h3>Đăng nhập</h3>
    <Bt10></Bt10>
    <h3>Todo List</h3>
    <Bt11></Bt11>
  </div>
</template>
<script setup>
import Bt01 from "./components/Bt01.vue";
import Bt02 from "./components/Bt02.vue";
import Bt03 from "./components/Bt03.vue";
import Bt04 from "./components/Bt04.vue";
import Bt05 from "./components/bt05.vue";
import Bt06 from "./components/bt06.vue";
import Bt07 from "./components/Bt07.vue";
import Bt08 from "./components/Bt08.vue";
import Bt09 from "./components/Bt09.vue";
import Bt10 from "./components/Bt10.vue";
import Bt11 from "./components/Bt11.vue";
</script>
<style></style>
