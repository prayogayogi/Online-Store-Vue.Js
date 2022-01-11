<template>
  <div class="home">
    <Navbar />

    <div class="container">
      <Hero />
      <div class="row mt-5">
        <div class="col">
          <h2>Best<strong></strong>Foods</h2>
        </div>
        <div class="col">
          <router-link to="/food" class="btn-sm btn-success float-right">
            <b-icon-eye></b-icon-eye> See all
          </router-link>
        </div>
      </div>

      <div class="row mb-3 mt-4">
        <div
          class="col col-md-4 col-12 mb-4"
          v-for="product in products"
          :key="product.id"
        >
          <card-product :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import Hero from "../components/Hero.vue";
import CardProduct from "../components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProducts(el) {
      this.products = el;
    },
  },
  created() {
    axios
      .get("http://localhost:3000/best-products")
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log("Data Gagal Di ambil", error));
  },
};
</script>


<style scoped>
.float-right {
  text-decoration: none;
}
</style>
