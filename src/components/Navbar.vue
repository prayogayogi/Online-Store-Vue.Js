<template>
<nav class="navbar navbar-expand-lg navbar-light">
  <div class="container">
      <a class="navbar-brand" href="/"><img src="https://uxwing.com/wp-content/themes/uxwing/download/20-food-and-drinks/meal-food.png" alt="logo" width="50px"></a>
    <button 
      class="navbar-toggler" 
      type="button" data-toggle="collapse" 
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
          <router-link class="nav-link" to="/keranjang">Keranjang
            <b-icon-bag class="ml-2 mr-1"></b-icon-bag>
            <span class="badge badge-success">0</span>
          </router-link>
        </li> 
      </ul>
    </div>
  </div>
</nav>
</template>

<script>
export default {
  name: 'Navbar'
}
</script>

<style>

</style>