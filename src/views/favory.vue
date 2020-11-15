<template>

  <div id="fav">

    <section v-if="token==undefined">
      <h3> You must log you first 🙃</h3>
    </section>
    <h1 v-else class="bigTitle">You're fav </h1>


    <section class="container">
      <div v-for="(data_fav, index) in data_fav" :key="index"  :id="index">
        <div v-if="data_fav !== null" class="card">
            <div class="content-image">
              <!--<img :id="images.id"  class="fullscreen" v-on:click="fullscreen(images.id)" v-if="images.type=='image/jpeg'||'image/png'" width="320" v-bind:src="images.link">
              <video class="fullscreen" v-else-if="images.type=='video/mp4'" controls width="320">
                <source :src="images.link"
                        type="video/mp4">
                Sorry, your browser doesn't support embedded videos.
              </video>-->
              <img v-bind:src="data_fav.link"  :alt="data_fav.title" width="320">

            </div>
          <h3  v-if="data_fav.title.length > 25"> {{ data_fav.title.substring(0,60) }}...</h3>
          <h3  v-else> {{ data_fav.title }}</h3>

        </div>

      </div>
    </section>
  </div>

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
