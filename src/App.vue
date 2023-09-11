<script setup>
</script>

<template>
  <nav
    class="navbar navbar-expand-lg navbar-dark bg-dark border-bottom border-body"
  >
    <div class="container-fluid">
      <routerLink to="/" class="navbar-brand">Rickpédia</routerLink>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item"><routerLink to="/" class="nav-link" aria-current="page">Home</routerLink></li>
        </ul>
      </div>
    </div>
  </nav>

  <div class="main">
    <router-view></router-view>
  </div>

  <footer class="bg-dark text-light">
    <div>Gabriel Rodrigues | ADS | {{ new Date().getFullYear() }}</div>
  </footer>

</template>

<style>
  footer{
    position: fixed;
    bottom: 0;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 56px;
    z-index: 5;
  }

  .main {
    margin-bottom: 80px;
  }
</style>
