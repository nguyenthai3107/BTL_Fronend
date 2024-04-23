<template>
    <div class="containPage">
      <div class="titlePage">
        <h2>
          Chào Mừng Đến Với
          <span class="titleWeb">KNOW<span class="text-dark">LIB</span></span>
        </h2>
      </div>
      <div class="contentPage">
        <!-- Section: Design Block -->
        <section class="">
          <!-- Jumbotron -->
          <div class="text-center text-lg-start">
            <div class="container">
              <div class="row gx-lg-5 align-items-center">
                <div class="col-lg-12 mb-5 mb-lg-0">
                  <h1 class="my-5 fw-bold ls-tight titleIntro">
                    Tâm hồn được nuôi dưỡng bởi
                    <span class="titleWeb"
                      >Những Quyển Sách.<span class="text-dark"></span
                    ></span>
                    <br />
                    <span class="auth">- William Shakespeare</span>
                  </h1>
                  <p style="color: hsl(217, 10%, 50.8%)">
                    Quyển sách là kho báu vô hình của nhân loại, mở ra trước mắt chúng ta 
                    một thế giới phong phú của tri thức, trí tưởng tượng và sự hiểu biết. 
                    Trong từng trang sách, chúng ta không chỉ phát hiện những điều kỳ diệu về thế giới xung quanh, 
                    mà còn tìm thấy những giá trị sâu thẳm trong mỗi con người.
                    Sách không chỉ là nguồn cảm hứng vô tận, mà còn là nguồn ánh sáng dẫn đường trong cuộc sống, 
                    là minh chứng cho sự tiến bộ không ngừng nghỉ của mỗi người chúng ta.
                  </p>
  
                  <router-link to="/about" class="text-decoration-none">
                    <button class="btnReadMore">Mượn Sách Ngay!</button>
                  </router-link>
                </div>
  
                <div class="col-lg-6 mb-5 mb-lg-0">
                  <div class="card">
                    <div class="imageCup">
                      <img src="../../../assets/bg-home.jpg" alt="" />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- Jumbotron -->
        </section>
        <!-- Section: Design Block -->
      </div>
    </div>
  </template>
  
  <script setup></script>
  
  <style lang="scss" scoped>
  @import "./Home.scss";
  </style>