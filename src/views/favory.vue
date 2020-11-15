<template>

  <section v-for="(data_fav, index) in data_fav" :key="index" class="card">

    <img v-bind:src="data_fav.link"  alt="">

    <h3> {{ data_fav.title }}</h3>

  </section>

</template>

<script>

export default {
name: "favory.vue",
  data() {
    return {
      token: null,
      data_fav: []
    }
  },
  beforeMount() {
    if (localStorage.getItem('token') == null) {
      console.log('nop');
    } else {
      console.log('yess');
      this.token = localStorage.getItem('token')
      fetch("https://api.imgur.com/3/account/testdev2004/favorites", {
        headers: {
          'Authorization': `Bearer ${this.token}`
        }
      }).then((rep) => rep.json()).then((repJSON) => {
        console.log(repJSON);
        this.data_fav = repJSON.data
        console.log(this.data_fav)

      });
    }
  }
}
</script>

<style scoped>

img{
  width: 200px;
}
</style>
