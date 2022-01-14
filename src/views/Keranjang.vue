<template>
  <div>
    <navbar :keranjangs="keranjangs" />
    <div class="container">
      <div class="row">
        <div class="col">
          <div class="row mt-3 breadcrumb">
            <nav aria-label="breadcrumb">
              <ol class="breadcrumb">
                <li class="breadcrumb-item">
                  <router-link to="/">Home</router-link>
                </li>
                <li class="breadcrumb-item">
                  <router-link to="/food">List Food</router-link>
                </li>
                <li class="breadcrumb-item active">
                  <strong>Keranjang</strong>
                </li>
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
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="`../asset/image/${keranjang.product.gambar}`"
                      :alt="keranjang.product.nama"
                      width="70px"
                    />
                  </td>
                  <td>{{ keranjang.product.nama }}</td>
                  <td>
                    {{
                      keranjang.keterangan
                        ? keranjang.keterangan
                        : "Description Not Found"
                    }}
                  </td>
                  <td>{{ keranjang.jumlahPesanan }}</td>
                  <td>{{ keranjang.product.harga }}</td>
                  <td>
                    {{ keranjang.product.harga * keranjang.jumlahPesanan }}
                  </td>
                  <td>
                    <a href="http://" class="btn-sm btn-info mr-2"
                      ><b-icon-pencil></b-icon-pencil
                    ></a>
                    <a
                      href="http://"
                      @click.prevent="hapusKeranjang(keranjang.id)"
                      class="btn-sm btn-danger"
                      ><b-icon-trash></b-icon-trash
                    ></a>
                  </td>
                </tr>

                <tr v-if="keranjangs.length >= 1">
                  <td colspan="6" align="right">
                    <strong>Total Harga : </strong>
                  </td>
                  <td>
                    <strong>Rp. {{ totalHarga }} </strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>

      <!-- Form Checkout -->
      <div class="row justify-content-end" v-if="keranjangs.length >= 1">
        <div class="col-md-4">
          <form @submit.prevent="checkout">
            <div class="form-group mt-3">
              <label for="nama">Nama: </label>
              <input
                type="text"
                class="form-control"
                v-model="pesan.nama"
                id="nama"
              />
            </div>
            <div class="form-group">
              <label for="keterangan">Nomer Meja</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.noMeja"
                id="keterangan"
              />
            </div>
            <button type="submit" class="btn btn-success flex-left">
              <b-icon-cart></b-icon-cart> Pesan
            </button>
          </form>
        </div>
      </div>
      <!-- End Form Checkout -->
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import axios from "axios";

export default {
  name: "keranjang",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      total: "",
      pesan: {},
    };
  },
  methods: {
    setKeranjang(data) {
      this.keranjangs = data;
    },
    totalPesanan(data) {
      this.total = data;
    },
    hapusKeranjang(id) {
      axios
        .delete(`http://localhost:3000/keranjangs/${id}`)
        .then(() => {
          alert("Data Berhasil Di Hapus");

          // Update Table Keranjang
          axios
            .get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjang(response.data))
            .catch((error) => console.log("Data Gagal Di ambil", error));
        })
        .catch((error) => console.log("Data Gagal Di Hapus", error));
    },
    checkout() {
      if (this.pesan.nama && this.pesan.noMeja) {
        this.pesan.keranjangs = this.keranjangs;

        // Hapus All Keranjang
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            this.keranjangs.forEach(function (item) {
              return axios
                .delete(`http://localhost:3000/keranjangs/${item.id}`)
                .catch((error) => console.log("Data Gagal Di Hapus", error));
            });

            this.$router.push({ path: "/pesanan-sukses" });
            alert("Pesanan anda berhasil di Checkout.");
          })
          .catch((error) => console.log("Data Gagal Di Push", error));
      } else {
        alert("Nama dan Nomor Meja Harus di Isi..!");
      }
    },
  },
  created() {
    axios
      .get("http://localhost:3000/keranjangs")
      .then((response) => this.setKeranjang(response.data))
      .catch((error) => console.log("Data Gagal Di ambil", error));
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.jumlahPesanan * data.product.harga;
      }, 0);
    },
  },
};
</script>

<style>
</style>