<template>
  <main>
    <div class="hero d-flex justify-content-center align-items-center">
      <div class="info text-center my-3">
        <h1 class="mb-2">Countries Informations</h1>
        <h3 class="mb-3">until we know each other</h3>
        <button class="btn"><a href="https://github.com/souf1neCoder" target="_blank">Github <i class="fab fa-github"></i></a></button>
      </div>
      <div class="open_search" @click="toggleSearchBar()">
        <span><i class="fa fa-search"></i></span>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  setup() {
    function toggleSearchBar() {
      const side = document.querySelector(".side");
      const main = document.querySelector(".main");
      const bar = document.querySelector(".open_search");
      side.classList.toggle("active");
      main.classList.toggle("active");
      bar.classList.toggle("active");
    }
    return {
      toggleSearchBar,
    };
  },
};
</script>

<style>
.hero {
  width: 100%;
  height: 45vh;
  overflow: hidden;
  background-image: url("~@/assets/images/bg.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  color: var(--light);
  position: relative;
}
.info {
  background: rgba(0, 0, 0, 0.66);
  padding: 30px;
  width: 55%;
}
.open_search {
  position: absolute;
  top: 0;
  left: 0;
  background-color: var(--light);
  margin-top: 2rem;
  width: 45px;
  height: 45px;
  text-align: center;
  display: none;
}
.open_search span {
  line-height: 45px;
}
.open_search span i {
  color: var(--primary-color);
  font-size: 1.2rem;
}
.btn{
  background-color:var(--light);
}
.btn a{
  color:var(--black);
}
.btn a:hover{
  text-decoration:none;
}
</style>