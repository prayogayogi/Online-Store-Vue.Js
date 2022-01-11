<template>
  <div class="row">
    <div class="col">
      <div class="card">
        <img :src="`../asset/image/${product.gambar}`" class="card-img-top" />
        <div class="card-body">
          <small class="font-weight-bold">Code: {{ product.kode }}</small>
          <h5 class="card-title">{{ product.nama }}</h5>
          <p>Price: Rp {{ product.harga }}</p>
          <router-link
            :to="'/food/' + product.id"
            class="btn-sm btn-success"
            v-if="product.is_ready"
          >
            <b-icon-cart></b-icon-cart> Ready
          </router-link>
          <a href="#" class="btn-sm btn-danger" v-else>Not Ready</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  name: "Card-product",
  data() {
    return {
      //
    };
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
