<template>
  <div id="nav">
<!--
    <MenuBurger/>
-->

    <router-link to="/">Home</router-link> |
    <router-link to="/login">Connection</router-link> |
    <router-link to="/favory">Favory</router-link>

  </div>
  <router-view/>
</template>

<script>

/*import MenuBurger from "@/components/menu";

export default {
  components: {MenuBurger}

}*/
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

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
