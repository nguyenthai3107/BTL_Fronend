<template>
    <div class="containPage">
      <h2>Đơn Mượn Sách</h2>
      <div class="contentPage">
        <div class="list-group">
          <div v-if="data.length === 0" class="orderEmpty">
            <img src="../../../public/Illustration/empty2.png" alt="" />
            <p>Chưa Có Đơn Mượn</p>
          </div>
          <div
            v-for="(order, index) in data"
            :key="order._id"
            class="list-group-item list-group-item-action mt-3 rounded"
          >
            <div class="d-flex">
              <h5>Chi Tiết Đơn Mượn:</h5>
              <a-dropdown class="ml-auto" v-if="order.TrangThai === 'W'">
                <a class="ant-dropdown-link" @click.prevent>
                  <i class="fa-solid fa-ellipsis-vertical fa-lg"></i>
                </a>
                <template #overlay>
                  <a-menu>
                    <a-menu-item>
                      <a @click="showModalDelete(order)"
                        ><i class="fa-solid fa-trash" style="color: red"></i
                      ></a>
                    </a-menu-item>
                  </a-menu>
                </template>
              </a-dropdown>
              <a-modal
                style="top: 40px"
                v-model:open="isModalDelete"
                title="Hủy Đơn Mượn"
                @ok="handleOkDelete()"
                :ok-button-props="okButtonProps"
                @cancel="handleCancelDelete"
                cancelText="Đóng"
                okText="Xác Nhận Hủy"
              >
                <p>Bạn có chắc muốn hủy đơn mượn ?</p>
              </a-modal>
            </div>
            <table class="table text-center">
              <thead>
                <tr class="table-borderless">
                  <th scope="col">STT</th>
                  <th scope="col">Tên Sách</th>
                  <th scope="col">Số Lượng</th>
                  <th scope="col">Đơn Giá/Ngày</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>{{ index + 1 }}</td>
                  <td>{{ order.MaSach.TenSach }}</td>
                  <td>{{ order.SoLuong }}</td>
                  <td>{{ order.MaSach.DonGia }} VND</td>
                </tr>
              </tbody>
            </table>
            <div class="d-flex">
              <div>
                <p>
                  Tổng Tiền Mượn:
                  <span style="color: #09896f; font-weight: bold"
                    >{{ order.ThanhTien }} VND</span
                  >
                </p>
                <p class="d-inline">
                  Ngày Mượn: {{ formatDateTime(order.NgayMuon) }}
                </p>
                <p class="d-inline ml-3" v-if="order.NgayMuon !== null">
                  Ngày Trả: {{ formatDateTime(order.NgayTra) }}
                </p>
              </div>
  
              <div
                v-if="order.TrangThai === 'A'"
                class="statusOrderSuccess mr-0 mb-0"
              >
                Đã Duyệt
              </div>
              <div
                v-else-if="order.TrangThai === 'D'"
                class="statusOrderDeny mr-0 mb-0"
              >
                Từ Chối
              </div>
              <div v-else class="statusOrderWait mr-0 mb-0">Chờ Duyệt</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  import axios from "axios";
  import { toast } from "vue3-toastify";
  import moment from "moment";
  const data = ref([]);
  const ID_DG = localStorage.getItem("ID_DG");
  const fetchData = () => {
    axios
      .get("http://localhost:3000/rent/user/" + ID_DG)
      .then((res) => {
        console.log(res.data);
        data.value = res.data;
      })
      .catch((err) => console.log(err));
  };
  fetchData();
  const formatDateTime = (dateTime) => {
    return moment(dateTime).format("DD-MM-YYYY HH:mm:ss");
  };
  const isModalDelete = ref(false);
  const idOrder = ref("");
  const showModalDelete = (order) => {
    isModalDelete.value = true;
    idOrder.value = order._id;
  };
  const handleCancelDelete = () => {
    isModalDelete.value = false;
  };
  const handleOkDelete = () => {
    axios
      .delete("http://localhost:3000/rent/" + idOrder.value)
      .then((res) => {
        if (res.data.error) {
          toast.error(res.data.error);
        } else {
          handleCancelDelete();
          fetchData();
          toast.success(res.data.message);
        }
      })
      .catch((err) => console.log(err));
  };
  const okButtonProps = {
    style: {
      background: "red", // Đặt màu đỏ cho nút "OK"
    },
  };
  </script>
  
  <style lang="scss" scoped>
  @import "./Order.scss";
  </style>