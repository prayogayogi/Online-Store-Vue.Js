<template>
  <div class="product">
    <Navbar />
    <div class="container">
    <!-- breadcrumb -->
      <div class="row mt-3 breadcrumb">
        <nav aria-label="breadcrumb">
          <ol class="breadcrumb">
            <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
            <li class="breadcrumb-item"><router-link to="/food">List Food</router-link></li>
            <li class="breadcrumb-item active"><strong>Detail Food</strong></li>
          </ol>
        </nav>
      </div>
      <div class="row">
        <div class="col">
          <img :src="'../asset/image/'+product.gambar" class="img-fluid shadow" alt="" width="500px">
        </div>
        <div class="col-md-6 mt-3">
          <h2><strong>{{ product.nama }}</strong></h2>
          <hr>
          <h4>Harga : <strong>Rp {{ product.harga }}</strong></h4>
          <form v-on:submit.prevent>
            <div class="form-group mt-3">
              <label for="jumlah">Jumlah Pesanan <strong>{{ jumlahPesanan }}</strong></label>
              <input type="number" class="form-control" v-model="pesan.jumlahPesanan" id="jumlah">
            </div>

            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea v-model="pesan.keterangan" class="form-control" id="keterangan" placeholder="Keterangan seperti Pedas, Ayam Geperek"></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan"><b-icon-cart></b-icon-cart> Pesan</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from "axios"


export default {
  name: "FoodDetail",
  components : {
    Navbar,
  },
  data(){
    return{
      product:[],
      pesan:{}
    }
  },
  methods: {
    setProducts(data){
      this.product = data
    },
    pemesanan(){
      if(this.pesan.jumlahPesanan){
        this.pesan.product = this.product;
        axios.
        post("http://localhost:3000/keranjangs", this.pesan)
            .then(() => {
              this.$router.push({ path: "/keranjang" })
              alert("Pesanan anda berhasil di pesan Silahkan tunggu..!");
            })
            .catch((error) => console.log("Data Gagal Di Push", error));
      }else{
        alert("Silahkan isi jumlah pesanan");
      }
    }
  },
  mounted() {
    axios.
     get("http://localhost:3000/products/"+this.$route.params.id)
    .then((response) => this.setProducts(response.data))
    .catch((error) => console.log("Data Gagal Di ambil", error));
  }
}
</script>

<style scoped>
  img{
    border-radius: 15px;
  }

</style>