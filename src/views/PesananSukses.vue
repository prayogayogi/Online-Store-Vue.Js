<template>
  <div class="sukses">
    <Navbar />
    <div class="container">
     <div class="row justify-content-center mt-4 mb-5">
       <div class="col text-center">
         <img src="../assets/image/menunggu.png" width="300" alt="">
         <h2><strong>Sukses.</strong></h2>
         <h4>Pesanan Anda Sedang Di Peroses <br> Mohon Di Tunggu.</h4>
       </div>
     </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
export default {
  name: "PesananSukses",
  components: { Navbar },
};
</script>

<style>
</style>