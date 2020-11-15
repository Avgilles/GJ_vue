<template>
  <div id="nav">
<!--
    <MenuBurger/>
-->

    <router-link to="/"><span class="home-nav"></span></router-link>
    <router-link to="/login"><span class="user-nav"></span></router-link>
    <router-link to="/favory"><span class="fav-nav"></span></router-link>

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
$font-style-title: 'Inter', 'Helvetica Neue', 'Helvetica', 'Arial', sans-serif;

$main-color: #000000;
$nav-bg : #634BBB;

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background: $main-color ;
  min-height: 100vh;
  font-family: Montserrat, sans-serif;
  margin: 0;
  font-family: $font-style-title;


}


#nav {
  position: fixed;
  left: 0;
  z-index: 50;
  display: flex;
  justify-content: space-around;
  flex-direction: column;
  height: 100vh;
  background: $nav-bg;
   a {
    font-size: 40px;
    color: #fff;
    text-decoration: none;
    padding: 20px;
    text-align: center;
  }


}
.container{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;

}


.card {
  min-width: 440px;
  min-height: 320px;
  background-color: white;
  margin: auto;
  margin: 20px;
  border-radius: 5px;
  position: relative;
  overflow: hidden;
}
.content{
/*  position: relative;
  top: 50%;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);*/
}
.content-image{
  max-height: 320px;
  overflow: hidden;
}
/*.coeur {
  width: 100%;
  align-self: flex-end;
}

.coeur:hover, .coeur:active {
  color: red;
  cursor: pointer;
}*/
h3{
  text-align: center;
  margin: auto;
  padding:  1em;
  max-width: 250px;
  color: #000000;
}


.bigTitle{
  text-transform: uppercase;
  -webkit-text-stroke-width: 2px;
  -webkit-text-stroke-color: rgb(255, 255, 255);
  font-size: 10vh;
  color: transparent;
  margin: 0;
}

.home-nav,
  {
  &:before{
    content: url("./assets/home-black.svg");
    /* background-image: url("./assets/home-black.svg");
     width: 50px;*/
  }
  &:hover:before{
    content: url("./assets/home-white.svg");

  }
}
.user-nav{
  &:before{
    content: url("./assets/user-black.svg");
    /* background-image: url("./assets/home-black.svg");
     width: 50px;*/
  }
  &:hover:before{
    content: url("./assets/user-white.svg");

  }
}
.fav-nav{
  &:before{
    content: url("./assets/star-black.svg");
    /* background-image: url("./assets/home-black.svg");
     width: 50px;*/
  }
  &:hover:before{
    content: url("./assets/star-white.svg");

  }
}

.fullscreen:-webkit-full-screen {
  width: auto !important;
  height: auto !important;
  margin:auto !important;
}
.fullscreen:-moz-full-screen {
  width: auto !important;
  height: auto !important;
  margin:auto !important;
}
.fullscreen:-ms-fullscreen {
  width: auto !important;
  height: auto !important;
  margin:auto !important;
}

</style>
