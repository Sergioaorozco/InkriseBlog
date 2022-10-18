<template>
  <nav class="navMain py-5 px-6">
    <div class="flex justify-between items-center wrapper">
      <a href="/"><figure class="navLogo bg-center"></figure></a>
      <figure class="md:hidden">
        <img width="36px" height="36px" src="../assets/mainLightLogo.svg" alt="mobile menu navigation">
      </figure>
      <ul class="hidden md:flex justify-between items-center gap-7 text-xl">
        <router-link to="/"> <li class="hover:border-b-2 text-gray-500 hover:text-purple-700 hover:border-purple-300">Inicio</li></router-link>
        <router-link to="/blog"> <li class="hover:border-b-2 text-gray-500 hover:text-purple-700 hover:border-purple-300">Blog</li></router-link>
        <li><a class="py-2 px-8 bg-amber-500 duration-300 hover:bg-purple-800 hover:duration-300 rounded-full text-gray-900 hover:text-white font-semibold " href="https://drive.google.com/file/d/12LUbSOtitrHSOtblaEWP13lgk6ZoDbgH/view?usp=sharing" target="_blank" rel="noopener noreferrer">Portfolio</a></li>
      </ul>
    </div>
  </nav>
   <router-view/>
</template>
<script>
</script>
<style scoped>
.navLogo {
  background-image: url("src/assets/mainDarkLogo.svg");
  background-repeat: no-repeat;
  height: 36px;
  width: 150px;
}
</style>