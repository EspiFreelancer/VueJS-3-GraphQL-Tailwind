<template>
  <div id="nav">
    <router-link to="/episodes">Episodes</router-link> |
    <router-link to="/locations">Locations</router-link> |
    <router-link to="/characters">Characters</router-link>
  </div>
  <router-view/>
  <hr>
  {{ info }}
  <hr>
  <router-link :to="prevComp">Prev</router-link> |
  <router-link :to="nextComp">Next</router-link>
</template>

<script setup> 
import { ref, provide, computed } from "vue";  
import { useRoute } from 'vue-router';

const info = ref({
  count: 0,
  pages: 0,
  next: 0,
  prev: 0,
});

provide("info", info);

const route = useRoute();

const prevComp = computed(() => ({
  name: route.name,
  params: { page: info.value.prev || route.params.page },
}))

const nextComp = computed(() => ({
  name: route.name,
  params: { page: info.value.next || route.params.page },
}))

console.log(prevComp);
console.log(nextComp);
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
