<script setup>
  import NavBar1 from "@/components/NavBar1.vue";

  const navbar1Elements = {
    classLight: '',
    classDark: '',
    menuElements: [
      { name: "Home", path: "/" },
      { name: "About", path: "/about" },
      {name: 'Files', submenu: [
        {name: 'File 1', path: '/file1'},
        {name: 'File 2', path: '/file2'}
      ]}
    ]
  }
</script>

<template>
  <NavBar1 
    :menuElements="navbar1Elements.menuElements" 
    :classDark="navbar1Elements.classDark" 
    :classLight="navbar1Elements.classLight" 
  ></NavBar1>
  
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
