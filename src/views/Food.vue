<template>
  <div>
    <Navbar />
    <div class="container">
      <div class="row">
        <div class="col">
          <h2>List<strong></strong> Foods</h2>
        </div>
      </div>
      <div class="row mt-2">
        <div class="col">
          <div class="input-group mb-3">
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Search Foods Favorite Yours."
              aria-label="Search Foods Favorite Yours."
              aria-describedby="basic-addon1"
              autofocus
              @keyup="searchFoods"
            />
            <span class="input-group-text" id="basic-addon1"
              ><b-icon-search></b-icon-search
            ></span>
          </div>
        </div>
      </div>
      <div class="row mb-3 mt-4">
        <div class="col col-md-4 col-12 mb-4" v-for="product in products" :key="product.id">
          <card-product :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardProduct from "../components/CardProduct.vue";
import Navbar from "../components/Navbar.vue";
import axios from "axios";

export default {
  name: "Food",
  components: {
    Navbar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  methods: {
    setProducts(el) {
      this.products = el;
    },
    searchFoods() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log("Data Gagal Di ambil", error));
    },
  },
  created() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log("Data Gagal Di ambil", error));
  },
};
</script>

<style scoped>
.card {
  border-radius: 10px;
}

.card-img-top {
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
}
</style>