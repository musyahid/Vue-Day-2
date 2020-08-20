<template>
  <div id="app">
    <HelloWorld msg="ALBUMS APPS"/>
    <div class="font-sans bg-grey-lighter flex flex-col min-h-screen w-full">
      <div class="flex-grow container mx-auto sm:px-4 pt-6 ">
        <div class="bg-white border-t border-b sm:border-l sm:border-r sm:rounded shadow mb-6">
          <div class="hidden lg:flex">
            <div class="w-1/2 text-center py-8">
                  <!-- This is an example component -->
              <div class="pt-2 relative mx-auto text-gray-600">
                <input class="border-2 border-gray-300 bg-white h-10 px-5 pr-16 rounded-lg text-sm focus:outline-none"
                  type="text" name="search" id="search" placeholder="search..." v-model="search">
        
              </div>
            </div>
          </div>
        </div>
        <div class="grid grid-flow-col grid-cols-3 grid-rows-3 gap-4">
          <div v-for="album of filteredAlbums" :key="album.id">
            <div class="max-w-sm rounded overflow-hidden shadow-lg">
              <img class="w-full" src="https://via.placeholder.com/600/92c952" alt="Sunset in the mountains">
              <div class="px-6 py-4">
                <div class="font-bold text-xl mb-2">{{album.title}}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      albums: [],
      search: ""
    }
  },
    async created() {
    try {
        const res = await axios.get(`http://localhost:3000/albums`);
        this.albums = res.data;
    } catch (e) {
        console.log(e)
    }
  },
  computed: {
    filteredAlbums: function() {
      return this.albums.filter((album) => {
          return album.title.match(this.search);
      });
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
