<template>
  <div class="containPage" v-if="isLogin">
    <h2>Danh Sách Thành Viên</h2>
    <div class="contentPage" :style="`${isLogin ? '' : 'display: none'}`">
      <a-tabs v-model:activeKey="activeKey">
        <a-tab-pane key="1" tab="Độc Giả">
          <h4>Danh Sách Độc Giả</h4>
          <a-table :dataSource="data" :columns="columns" rowKey="_id">
          </a-table>
        </a-tab-pane>
        <a-tab-pane key="2" tab="Nhân Viên/Quản Lý" force-render>
          <h4>Danh Sách Nhân Viên/Quản Lý</h4>
          <a-table :dataSource="dataStaff" :columns="columnsStaff" rowKey="_id">
          </a-table>
        </a-tab-pane>
      </a-tabs>
    </div>
  </div>
  <div v-else class="denied">
    <h3 class="text-center mt-5">Vui lòng đăng nhập tài khoản để thao tác.</h3>
  </div>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const activeKey = ref("1");
const data = ref([]);
const dataStaff = ref([]);

const isLogin = localStorage.getItem("isLogin");

const columns = [
  {
    title: "ID Độc Giả",
    dataIndex: "_id",
    key: "_id",
  },
  {
    title: "Họ Tên",
    dataIndex: "Ten",
    key: "Ten",
  },
  {
    title: "Ngày Sinh",
    dataIndex: "NgaySinh",
    key: "NgaySinh",
  },
  {
    title: "Giới Tính",
    dataIndex: "Phai",
    key: "Phai",
  },
  {
    title: "Số Điện Thoại",
    dataIndex: "DienThoai",
    key: "DienThoai",
  },
  {
    title: "Địa Chỉ",
    dataIndex: "DiaChi",
    key: "DiaChi",
  },
];

const columnsStaff = [
  {
    title: "ID Nhân Viên/Quản Lý",
    dataIndex: "_id",
    key: "_id",
  },
  {
    title: "Họ Tên",
    dataIndex: "HoTenNv",
    key: "HoTenNv",
  },
  {
    title: "Chức Vụ",
    dataIndex: "ChucVu",
    key: "ChucVu",
  },
  {
    title: "Số Điện Thoại",
    dataIndex: "SoDienThoai",
    key: "SoDienThoai",
  },
  {
    title: "Địa Chỉ",
    dataIndex: "DiaChi",
    key: "DiaChi",
  },
];

const fetchData = () => {
  axios
    .get("http://localhost:3000/reader")
    .then((res) => {
      data.value = res.data;
    })
    .catch((err) => console.log(err));
};

const fetchDataStaff = () => {
  axios
    .get("http://localhost:3000/reader/admin")
    .then((res) => {
      dataStaff.value = res.data;
    })
    .catch((err) => console.log(err));
};

fetchData();
fetchDataStaff();
</script>

<style lang="scss" scoped>
@import "./Customer.scss";
</style>