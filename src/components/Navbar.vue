<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <router-link to="/">
          <img
            src="https://uxwing.com/wp-content/themes/uxwing/download/20-food-and-drinks/meal-food.png"
            alt="logo"
            width="50px"
        /></router-link>
        <b-navbar-toggle target="nav-collapse"> </b-navbar-toggle>
        <b-collapse id="nav-collapse" is-nav>
          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <router-link class="nav-link" to="/">Home</router-link>
            <router-link class="nav-link" to="/food">Food</router-link>
            <router-link class="nav-link" to="/keranjang">
              <b-icon-bag class="ml-n1 mr-1"></b-icon-bag>
              <span class="badge badge-success">{{
               keranjangs ? keranjangs.length : keranjang_pesanan.length
              }}</span>
            </router-link>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
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
  props: ['keranjangs'],
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