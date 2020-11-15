<template>
  <div class="home">

    <section v-for="(data_imgur, index) in data_imgur" :key="index" class="card" :id="index">
      <!--<div v-for="(images, index) in data_imgur.images" :key="index" >
        <img v-if="images.type=='image/jpeg'||'image/png'" width="200" v-bind:src="images.link" alt="">
        <video v-else-if="images.type=='video/mp4'" controls width="200">
          <source :src="images.link"
                  type="video/mp4">
          Sorry, your browser doesn't support embedded videos.
        </video>

        <button :id="images.id"  v-on:click="addFavory(images.id)" class="btn-secondary like-review">
          <i  class="fa fa-heart" aria-hidden="true"></i> Like
        </button>
      </div>-->
      <h3> {{ data_imgur.title }}</h3>
      <p>{{data_imgur.topic}}</p>

      <div id="demo" class="carousel slide carousel-fade" data-ride="carousel">
        <!-- Indicateurs -->
        <ul class="carousel-indicators">
          <li data-target="#demo" data-slide-to="0" class="active"></li>
          <li data-target="#demo" data-slide-to="1"></li>
          <li data-target="#demo" data-slide-to="2"></li>
        </ul>

        <!-- Carrousel -->
        <div class="carousel-inner">
          <div class="carousel-item active" data-interval="4000">
            <img src="https://www.pierre-giraud.com/bootstrap-carrousel-slide-1.jpg" alt="Carrousel slide 1" class="d-block w-100">
          </div>
          <div class="carousel-item" data-interval="2000">
            <img src="https://www.pierre-giraud.com/bootstrap-carrousel-slide-2.jpg" alt="Carrousel slide 2" class="d-block w-100">
          </div>
          <div class="carousel-item" data-interval="1000">
            <img src="https://www.pierre-giraud.com/bootstrap-carrousel-slide-3.jpg" alt="Carrousel slide 3" class="d-block w-100">
          </div>
        </div>

        <!-- Contrôles -->
        <a class="carousel-control-prev" href="#demo" role="button" data-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="sr-only">Précédent</span>
        </a>
        <a class="carousel-control-next" href="#demo" role="button" data-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="sr-only">Suivant</span>
        </a>
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
      window.location.href = '/connection'
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
    }
  }
}


</script>

<style scoped>
.card {
  margin: 1.2rem;
  width: 200px;
  border: solid 1px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.coeur {
  width: 100%;
  align-self: flex-end;
}

.coeur:hover, .coeur:active {
  color: red;
  cursor: pointer;
}

</style>
