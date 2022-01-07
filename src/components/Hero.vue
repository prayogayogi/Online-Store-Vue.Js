<template>
  <div>
    <div class="container">
      <div class="row mt-5">
        <div class="col-md align-self-center">
          <h2><strong>Delicius Food Menu</strong><br />In Your Gadget</h2>
          <p class="mt-3">Come on, order your food before you're hungry</p>
          <router-link to="/food"  class="btn btn-success btn-sm mt-3">
            <b-icon-arrow-right></b-icon-arrow-right> Order
          </router-link>
        </div>
        <div class="col-md">
          <img src="../assets/image/breakfast.svg" alt="" width="400px" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero"
};
</script>

<style>
</style>