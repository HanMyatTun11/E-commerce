<template>
    <div class="container-fluid bg-dark">
        <nav class="container navbar navbar-expand-lg navbar-light">
  <div class="container-fluid">
    <router-link class="navbar-brand text-white" to="/">
        <i class="material-icons me-2">home</i>
        <span>BM E-Commerce</span>
    </router-link>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link active text-white" aria-current="page" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link text-white" href="#">
            <i class="material-icons">shopping_cart</i>
            <span class="cardItems">{{ cartCount }}</span>
          </a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle text-white" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            User
          </a>
          <ul class="dropdown-menu">
            <li v-if="logged"><a class="dropdown-item" href="#">Logout</a></li>
            <li v-if="!logged"><router-link class="dropdown-item" to="/login">Login</router-link></li>
            <li v-if="!logged"><router-link class="dropdown-item" to="/register">Register</router-link></li>
          
          </ul>
        </li>
      </ul>
    </div>
  </div>
</nav>
    </div>
</template>

<script>
export default {
  props:['logged','cartCount']
}
</script>

<style>
.cardItems{
  background: red;
  font-size: 12px;
  border-radius: 50%;
  padding: 5px;
}
</style>