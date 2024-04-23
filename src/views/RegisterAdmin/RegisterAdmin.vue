<template>
    <div class="containPage">
      <section>
        <div class="container h-100">
          <div class="row d-flex justify-content-center align-items-center h-100">
            <div class="col col-xl-20">
              <div class="card loginForm">
                <div class="row g-0">
                  <div class="col-md-6 col-lg-6 d-flex align-items-center">
                    <div class="card-body p-4 p-lg-4 text-black">
                      <form
                        method="post"
                        @submit.prevent="register"
                        enctype="multipart/form-data"
                      >
                        <div class="d-flex align-items-center mb-3 pb-1">
                          <div class="logo">
                            <img src="../../assets/logoBook.png" alt="" />
                            <span class="titleWeb"
                              >KNOW<span class="text-dark">LIB</span></span
                            >
                          </div>
                        </div>
  
                        <div class="fw-normal pb-2 desLogin">
                          Đăng Ký Tài Khoản Nhân Viên
                        </div>
  
                        <div class="group">
                          <label for="phone"
                            ><i class="fa-solid fa-phone iconForm"></i
                          ></label>
                          <input
                            type="text"
                            id="phone"
                            name="phone"
                            class="groupInput"
                            autocomplete="off"
                            v-model="phone"
                            placeholder="Số điện thoại"
                            required
                          />
                        </div>
                        <div class="group">
                          <label for="username"
                            ><i class="fa-solid fa-user iconForm"></i
                          ></label>
                          <input
                            type="text"
                            id="username"
                            name="username"
                            v-model="username"
                            class="groupInput"
                            autocomplete="off"
                            placeholder="Họ Tên"
                            required
                          />
                        </div>
  
                        <div class="group2">
                          <label for="password"
                            ><i class="fa-solid fa-lock iconForm"></i
                          ></label>
                          <input
                            :type="showPassword ? 'text' : 'password'"
                            v-model="password"
                            name="password"
                            id="password"
                            class="groupInput"
                            autocomplete="off"
                            placeholder="Mật Khẩu"
                            required
                          />
                          <div @click="toggleShowPassword" class="iconPassword">
                            <div v-if="showPassword">
                              <i class="fa-solid fa-eye"></i>
                            </div>
                            <div v-else>
                              <i class="fa-solid fa-eye-slash"></i>
                            </div>
                          </div>
                        </div>
  
                        <div class="group">
                          <label for="position"
                            ><i class="fa-solid fa-user-tie iconForm"></i
                          ></label>
                          <select
                            class="selectGroup"
                            v-model="position"
                            name="postion"
                            id="position"
                            required
                          >
                            <option value="">Chọn Chức Vụ</option>
                            <option value="Quản lý">Quản Lý</option>
                            <option value="Nhân viên">Nhân Viên</option>
                          </select>
                        </div>
  
                        <div class="group">
                          <label for="address"
                            ><i class="fa-solid fa-map iconForm"></i
                          ></label>
                          <input
                            type="text"
                            id="address"
                            name="address"
                            v-model="address"
                            class="groupInput"
                            autocomplete="off"
                            placeholder="Địa Chỉ"
                            required
                          />
                        </div>
  
                        <div class="group">
                          <label for="avatar"
                            ><i class="fa-solid fa-image iconForm"></i
                          ></label>
                          <input
                            type="file"
                            id="avatar"
                            class="groupInput"
                            autocomplete="off"
                            name="avatar"
                            accept="image/jpeg, image/png, image/jpg"
                            required
                            ref="imageInput"
                            @change="handleFileUpload"
                          />
                        </div>
                        <div class="pt-1 mb-4">
                          <button class="btnPay" type="submit">Đăng Ký</button>
                        </div>
                        <p class="mb-1 pb-lg-2" style="color: #09896f;">
                          Đã có tài khoản?
                          <router-link to="/admin/login" class="button">
                            <strong style="color: #09896f;">Đăng Nhập</strong>
                          </router-link>
                        </p>
                      </form>
                    </div>
                  </div>
                  <div class="col-md-6 col-lg-6 d-none d-md-block m-auto">
                    <img
                      src="https://phunugioi.com/wp-content/uploads/2021/11/Background-book-sach-tren-gia.jpg"
                      alt="login form"
                      class="imageLogin"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </template>
  
<script setup>
    import axios from "axios";
    import { ref } from "vue";
    import { toast } from "vue3-toastify";
    import { useRouter } from "vue-router";
    const router = useRouter();
    const phone = ref("");
    const username = ref("");
    const password = ref("");
    const address = ref("");
    const position = ref("");
    const avatar = ref(null);
    const showPassword = ref(false);
    const toggleShowPassword = () => {
        showPassword.value = !showPassword.value;
    };
    const handleFileUpload = (e) => {
        avatar.value = e.target.files[0];
    };
    const register = async () => {
        const formData = new FormData();
        formData.append("avatar", avatar.value);
        formData.append("username", username.value);
        formData.append("phone", phone.value);
        formData.append("password", password.value);
        formData.append("position", position.value);
        formData.append("address", address.value);
        axios
        .post("http://localhost:3000/authentication/register/staff", formData)
        .then((res) => {
            if (res.data.error) {
            toast.error(res.data.error);
            } else {
            router.push("/admin/login");
            }
        })
        .catch((err) => console.log(err));
    };
</script>
<style lang="scss" scoped>
  @import "./RegisterAdmin.scss";
</style>