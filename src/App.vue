<template>
  <nav class="navMain bg-purple-900 py-5 px-6">
    <div class="flex justify-between items-center wrapper">
      <router-link to="/"><figure class="navLogo bg-center"></figure></router-link>
      <figure class="md:hidden" @click="popUpMenu">
        <img class="w-10" src="../src/assets/navLightMobile.svg" alt="mobile menu navigation">
      </figure>
      <ul class="hidden md:flex justify-between items-center gap-7 text-xl">
        <router-link to="/"> <li class="hover:border-b-2 text-white hover:text-purple-300 hover:border-purple-300">Inicio</li></router-link>
        <router-link to="/blog"> <li class="hover:border-b-2 text-white hover:text-purple-300 hover:border-purple-300">Blog</li></router-link>
        <li><a class="py-2 px-8 bg-purple-200 duration-300 hover:bg-white hover:duration-300 rounded-full text-gray-900 font-semibold " href="https://drive.google.com/file/d/12LUbSOtitrHSOtblaEWP13lgk6ZoDbgH/view?usp=sharing" target="_blank" rel="noopener noreferrer">Portfolio</a></li>
      </ul>
    </div>
    <div v-if="isMobileActive" class="z-50 fixed bottom-0 right-0 top-0 bg-white w-full h-screen list-none px-5 py-10">
      <nav class="flex flex-col gap-10 text-center">
        <figure @click="closeMenu">
          <img class="w-10 float-right" src="../src/assets/navCloseMobile.svg" alt="mobile menu navigation">
        </figure>
        <router-link @click="closeMenu" to="/"> <li class="text-5xl text-black">Inicio</li></router-link>
        <hr>
        <router-link @click="closeMenu" to="/blog"> <li class="text-5xl text-black">Blog</li></router-link>
        <hr>
        <li><a class="py-2 w-full px-8 text-5xl bg-purple-200 rounded-full text-gray-900" href="https://drive.google.com/file/d/12LUbSOtitrHSOtblaEWP13lgk6ZoDbgH/view?usp=sharing" target="_blank" rel="noopener noreferrer">Portfolio</a></li>
      </nav>
    </div>
  </nav>
  <router-view/>
</template>

<style scoped>
.navLogo {
  background-image: url("../src/assets/mainLightLogo.svg");
  background-repeat: no-repeat;
  height: 36px;
  width: 150px;
}
</style>

<script>
export default {
  data(){
    return {
      isMobileActive : false
    }
  },
  methods: {
    popUpMenu() {
      this.isMobileActive = true
    },
    closeMenu() {
      this.isMobileActive = false
    }
  }
}
</script>
