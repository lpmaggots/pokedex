<template>
  <nav class="navbar bg-dark navbar-light navbar-expand-lg" data-bs-theme="dark">
    <div class="container">
      <router-link class="navbar-brand d-flex" to="/">
        <img src="https://cdn-icons-png.flaticon.com/512/188/188987.png" width="30">
        <div class="px-1"></div>
        <span>Pokedex</span>
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbar" aria-controls="navbar" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbar">
        <ul class="navbar-nav me-auto my-2 my-lg-0">
          <li class="nav-item">
            <router-link class="nav-link" aria-current="page" to="/" exact-active-class="active">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about" exact-active-class="active">About</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>