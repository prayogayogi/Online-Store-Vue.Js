<template>
  <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container">
      <router-link class="navbar-brand" to="/">
        <img
          src="https://uxwing.com/wp-content/themes/uxwing/download/20-food-and-drinks/meal-food.png"
          alt="logo"
          width="50px"
        />
      </router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/food">Food</router-link>
          </li>
        </ul>
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link" to="/keranjang">
              <b-icon-bag class="ml-n1 mr-1"></b-icon-bag>
              <span class="badge badge-success">{{
                keranjang_pesanan.length
              }}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",
  data() {
    return {
      keranjang_pesanan: [],
    };
  },
  methods: {
    getKeranjang(data) {
      this.keranjang_pesanan = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.getKeranjang(response.data))
      .catch((error) => console.log("Data Gagal Di ambil", error));
  },
};
</script>

<style>
</style>