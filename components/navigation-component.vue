<template>
  <nav class="nav-container absolute z-50 sticky top-0 flex items-center justify-between flex-wrap bg-red-700 p-6 text-white" :class="{onScrollColor: scrollPosition > 50}">
    <div class="flex items-center flex-shrink-0 mr-6">
      <img src="/pokeball.svg" class="w-10" alt="book lover">
      &nbsp;
      <span class="font-semibold text-lg tracking-tight">Pokedex</span>
    </div>
    <div class="block lg:hidden">
      <button @click="toggle" class="flex px-3 py-2 border rounded border-black focus:outline-none">
        <svg class="fill-current h-3 w-3" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
      </button>
    </div>
    <div class="w-full block flex-grow lg:flex lg:items-center lg:w-auto" :class="open ? 'block': 'hidden'">
      <div class="text-sm lg:flex-grow">
      </div>
      <div class="tracking-tight">
        <form v-on:submit.prevent="searchPokemon">
          <n-link to="/" class="block mt-4 lg:inline-block lg:mt-0 hover:underline mr-4 focus:outline-none">
            Pokemon List
          </n-link>
          <input class="border-2 border-gray-300 bg-white h-10 pl-2 pr-8 rounded-lg text-black text-sm focus:outline-none" v-model="searchedText" type="search" name="search" placeholder="Search">
        </form>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  data() {
    return {
      open: false,
      scrollPosition: null,
      searchedText: '',
    };
  },
  mounted() {
    window.addEventListener('scroll', this.updateScroll);
  },
  methods:{
    toggle() {
    	this.open = !this.open
    },
    updateScroll() {
       this.scrollPosition = window.scrollY
    },
    searchPokemon(){
      if(this.searchedText == ''){
        this.$router.push({ path: '/'}); 
      }else{
        this.$router.push({ path: '/pokemon', query: { pokemon: this.searchedText.toLowerCase() }}); 
      }
    }
  }
}
</script>
<style scoped>
  @media screen and (min-width: 1025px) {
    .nav-container{
      padding-left: 15rem;
      padding-right: 15rem;
    }
  }

  .onScrollColor {
    -moz-transition: all .2s ease-in;
    -o-transition: all .2s ease-in;
    -webkit-transition: all .2s ease-in;
    transition: all .2s ease-in;
    opacity: 90%;
    background-color: white !important;
    color: black
  }
</style>