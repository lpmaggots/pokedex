<template>
  <div class="container pt-3">
    <section class="row">
      <div class="col">
        <h2>🇧🇷 Sobre o Projeto</h2>
        <p>
          Este é um aplicativo desenvolvido com Vue 3 e Vite, utilizando Bootstrap 5 para a interface de usuário. O projeto foi criado para ser leve, rápido e responsivo, oferecendo uma experiência fluida e intuitiva. A arquitetura é baseada na Composition API, garantindo uma melhor organização e reutilização de código. <br>
          Para buscar dados sobre os Pokémons, foi integrado ao projeto o uso da <a href="https://pokeapi.co/" target="_blank">PokeAPI</a>, uma API pública que fornece informações detalhadas sobre a franquia Pokémon. Essa integração permitiu a exibição dinâmica de dados como nome, número, tipo e habilidades dos Pokémons. Este projeto demonstra minhas habilidades com Vue.js 3, componentização, desenvolvimento escalável, design responsivo e integração com APIs externas.</p>
        <hr class="mt-6 mb-5" />
        <h2>🇺🇸 About the Project</h2>
        <p>This is an application developed with Vue 3 and Vite, using Bootstrap 5 for the user interface. The project was designed to be lightweight, fast, and responsive, providing a smooth and intuitive experience. The architecture is based on the Composition API, ensuring better code organization and reusability. <br>
          To retrieve data about Pokémon, I integrated the project with the <a href="https://pokeapi.co/" target="_blank">PokeAPI</a>, a public API that provides detailed information about the Pokémon franchise. This integration allowed dynamic display of data such as name, number, type, and abilities of the Pokémon. This project showcases my skills in Vue.js 3, componentization, scalable development, responsive design, and integration with external APIs.</p>
      </div>
    </section>
    <section class="row">
      <div class="col text-center mt-4">
        <h2 class="mb-5">Tecnologias utilizadas | Used technologies</h2>
        <div class="row">
          <div v-for="(logo, index) in logos" :key="index" class="col d-flex justify-content-center align-items-center">
            <img :src="logo.path" :alt="logo.name" :width="logo.name == 'Pokeapi' ? null : '120'" height="120" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
  const logos = [
    { name: 'Vue', path: '/vue-logo.png' },
    { name: 'Vite', path: '/vite-logo.png' },
    { name: 'Bootstrap', path: '/bootstrap-logo.png' },
    { name: 'PWA', path: '/pwa-logo.png' },
    { name: 'Pokeapi', path: '/pokeapi-logo.png' },
  ]
</script>