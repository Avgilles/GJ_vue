<template>
  <div class="home">
    <section v-if="token==undefined">
      <h3> You must log you first 🙃</h3>
    </section>
    <h1 v-else class="bigTitle">be viral </h1>

    <section class="container">
      <div v-for="(data_imgur, index) in data_imgur" :key="index"  :id="index">
        <div v-if="data_imgur !== null" class="card">

          <div class="content" v-for="(images, index) in data_imgur.images" :key="index" >
            <div class="content-image">



              <img :id="images.id"  class="fullscreen" v-on:click="fullscreen(images.id)" v-if="images.type=='image/jpeg'||'image/png'" width="320" v-bind:src="images.link">
              <video class="fullscreen" v-else-if="images.type=='video/mp4'" controls width="320">
                <source :src="images.link"
                        type="video/mp4">
                Sorry, your browser doesn't support embedded videos.
              </video>
            </div>


          </div>
          <h3 v-if="data_imgur.title.length > 25"> {{ data_imgur.title.substring(0,60) }}..</h3>
          <h3 v-else>{{ data_imgur.title}}</h3>
          <button v-on:click="addFavory(data_imgur.images[0].id)" class="btn-secondary like-review">
            <i  class="fa fa-heart" aria-hidden="true"></i> Like
          </button>

        </div>

      </div>
    </section>
  </div>
</template>

<script>


export default {
  name: 'Home',
  data() {
    return {
      token: null,
      data_imgur: [],
      idImage : null
    }
  },
  beforeMount() {
    if (localStorage.getItem('token') == null) {
      console.log('nop');
    } else {
      console.log('yess');
      this.token = localStorage.getItem('token')

      fetch("https://api.imgur.com/3/gallery/hot/viral/0.json", {
        headers: {
          'Authorization': `Bearer ${this.token}`
        }
      }).then((rep) => rep.json()).then((repJSON) => {
        console.log(repJSON);
        this.data_imgur = repJSON.data
      });
    }
  },methods: {
    addFavory: function (x) {

      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer ${this.token}`);

      var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch(`https://api.imgur.com/3/image/${x}/favorite`, requestOptions)
          .then(response => response.text())
          .then(result => console.log(result))
          .catch(error => console.log('error', error));
    },
    fullscreen : function (z){
      let divObj = document.getElementById(z);
      //Use the specification method before using prefixed versions
      if (divObj.requestFullscreen) {
        divObj.requestFullscreen();

      }

      else if (divObj.msRequestFullscreen) {
        divObj.msRequestFullscreen();
      }
      else if (divObj.mozRequestFullScreen) {
        divObj.mozRequestFullScreen();
      }
      else if (divObj.webkitRequestFullscreen) {
        divObj.webkitRequestFullscreen();
      } else {
        console.log("Fullscreen API is not supported");
      }
      document.onclick = function () {
        if (document.fullscreenElement) {
          document.exitFullscreen()
        }
      }
    }
  }
}


</script>

<style lang="scss" scoped>


</style>
