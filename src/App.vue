<script></script>
<template>
  <header>
    <router-link class="btn-nav" :to="{ name: 'home' }">Home</router-link>
    <router-link class="btn-nav" to="/categorias">Categorias</router-link>
    <router-link class="btn-nav" to="/editoras">Acessorios</router-link>
    <router-link class="btn-nav" to="/autores">Autores</router-link>
    <router-link class="btn-nav" to="/livros">Livros</router-link>
  </header>
  <main>
    <RouterView />
    <img src="../src/assets/brabo.gif" alt="sex" />
  </main>
</template>
<style scoped>
.btn-nav {
  text-decoration: none;
  color: rgb(189, 0, 0);
  font-size: 20px;
  background-color: #000;
  padding: 10px;
  border-radius: 5px;
  transition: 0.1s;
  display: inline-block;
  margin-right: 10px;
}

.btn-nav:hover {
  color: black;
  background-color: rgb(189, 0, 0);
  transform: scale(1.3);
  z-index: 1;
}

.btn-nav:active {
  color: black;
  background-color: rgb(189, 0, 0);
  transform: scale(0.9);
}
</style>
