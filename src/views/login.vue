<template>
  <div class="connect">
    <section v-if="token==undefined">
      <h3> Great choice 👌</h3>
      <a class="loginButton" href="https://api.imgur.com/oauth2/authorize?client_id=d33f24daaee4a85&response_type=token">Se connecter</a>
    </section>
    <section v-else>
      <img :src="data_profil.avatar" alt="">
      <h3>{{data_profil.url}}</h3>
    </section>

  </div>
</template>

<script>

function getToken (){
  var vars = {};
  var replacePart = window.location.href.replace(/[?&]+([^=&]+)=([^&]*)/gi, function (m, key, value){
    vars[key] = value;
  });
  console.log(replacePart)
  return vars;
}
export default{
  name: 'login',
  data() {
    return {
      token: null,
      data_profil: [],
    }
  },
  beforeMount() {
    let tokn = getToken().access_token;
    if(tokn){
      localStorage.setItem('token', tokn);
      window.location.href="/Home"

    }

    if (localStorage.getItem('token') == null) {
      console.log('nop');
    } else {
      console.log('yess');
      this.token = localStorage.getItem('token')

      fetch("https://api.imgur.com/3/account/testdev2004", {
        headers: {
          'Authorization': `Bearer ${this.token}`
        }
      }).then((rep) => rep.json()).then((repJSON) => {
        console.log(repJSON);
        this.data_profil = repJSON.data
        console.log(this.data_profil)
      });

    }

  }


}
</script>


<style lang="scss" scoped>
.loginButton{
  margin: 10px;
  padding: 1em;
  display: inline-block;
  text-transform: uppercase;
  border-radius: 5px;
  text-decoration: none;
  color: white;
  border: solid 1px white;
  transition: 0.5s;
  &:hover{
    background-color: #634bbb;
  }
}
</style>
