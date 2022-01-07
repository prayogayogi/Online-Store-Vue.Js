<template>
  <div>
    <navbar />
    <div class="container">
      <div class="row">
        <div class="col">
          <div class="row mt-3 breadcrumb">
            <nav aria-label="breadcrumb">
              <ol class="breadcrumb">
                <li class="breadcrumb-item"><router-link to="/">Home</router-link></li>
                <li class="breadcrumb-item"><router-link to="/food">List Food</router-link></li>
                <li class="breadcrumb-item active"><strong>Keranjang</strong></li>
              </ol>
            </nav>
          </div>
        </div>
      </div>
      <div class="row ml-2">
        <div class="col mt-n4">
          <h4>Keranjang <strong>Saya</strong></h4>
          <div class="table-responsive mt-4">
            <table class="table table-hover">
              <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Photo</th>
                <th scope="col">Makan</th>
                <th scope="col">Keterangan</th>
                <th scope="col">Jumlah</th>
                <th scope="col">Harga</th>
                <th scope="col">Total</th>
                <th scope="col">Aksi</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                <th>{{ index+1 }}</th>
                <td>
                  <img :src="`../asset/image/${keranjang.product.gambar}`" :alt="keranjang.product.nama" width="70px">
                </td>
                <td>{{ keranjang.product.nama }}</td>
                <td v-if="keranjang.keterangan">{{ keranjang.keterangan }}</td>
                <td v-else class="text-danger">Tidak ada deskripsi</td>
                <td>{{ keranjang.jumlahPesanan }}</td>
                <td>{{ keranjang.product.harga }}</td>
                <td>{{ keranjang.product.harga * keranjang.jumlahPesanan}}</td>
                <td>
                  <a href="http://" class="btn-sm btn-info mr-2"><b-icon-pencil></b-icon-pencil></a>
                  <a href="http://" class="btn-sm btn-danger"><b-icon-bag-x ></b-icon-bag-x></a>
                </td>
              </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue'
import axios from "axios";


export default {
  name:'keranjang',
  components: {
    Navbar ,
  },
  data(){
    return{
      keranjangs: [],
      total:''
    }
  },
  methods:{
    setKeranjang(data){
      this.keranjangs = data
    },
    totalPesanan(data){
      this.total = data
    }
  },
  created() {
    axios.
       get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjang(response.data))
      .catch((error) => console.log("Data Gagal Di ambil", error))
  }

}
</script>

<style>

</style>