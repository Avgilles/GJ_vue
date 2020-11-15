<template>
  <div class="connect">
    <section v-if="token==undefined">
      <h2>Connecte toi !</h2>
      <a href="https://api.imgur.com/oauth2/authorize?client_id=d33f24daaee4a85&response_type=token">Se connecter</a>
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
      window.location.href = '/connection'
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


<style scoped>
@import url(https://fonts.googleapis.com/css?family=Roboto:300);

.login-page {
  width: 360px;
  padding: 8% 0 0;
  margin: auto;
}
.form {
  position: relative;
  z-index: 1;
  background: #FFFFFF;
  max-width: 360px;
  margin: 0 auto 100px;
  padding: 45px;
  text-align: center;
  box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2), 0 5px 5px 0 rgba(0, 0, 0, 0.24);
}
.form input {
  font-family: "Roboto", sans-serif;
  outline: 0;
  background: #f2f2f2;
  width: 100%;
  border: 0;
  margin: 0 0 15px;
  padding: 15px;
  box-sizing: border-box;
  font-size: 14px;
}
.form button {
  font-family: "Roboto", sans-serif;
  text-transform: uppercase;
  outline: 0;
  background: #4CAF50;
  width: 100%;
  border: 0;
  padding: 15px;
  color: #FFFFFF;
  font-size: 14px;
  -webkit-transition: all 0.3 ease;
  transition: all 0.3 ease;
  cursor: pointer;
}
.form button:hover,.form button:active,.form button:focus {
  background: #43A047;
}
.form .message {
  margin: 15px 0 0;
  color: #b3b3b3;
  font-size: 12px;
}
.form .message a {
  color: #4CAF50;
  text-decoration: none;
}
.form .register-form {
  display: none;
}
.container {
  position: relative;
  z-index: 1;
  max-width: 300px;
  margin: 0 auto;
}
.container:before, .container:after {
  content: "";
  display: block;
  clear: both;
}
.container .info {
  margin: 50px auto;
  text-align: center;
}
.container .info h1 {
  margin: 0 0 15px;
  padding: 0;
  font-size: 36px;
  font-weight: 300;
  color: #1a1a1a;
}
.container .info span {
  color: #4d4d4d;
  font-size: 12px;
}
.container .info span a {
  color: #000000;
  text-decoration: none;
}
.container .info span .fa {
  color: #EF3B3A;
}
body {
  background: #76b852; /* fallback for old browsers */
  background: -webkit-linear-gradient(right, #76b852, #8DC26F);
  background: -moz-linear-gradient(right, #76b852, #8DC26F);
  background: -o-linear-gradient(right, #76b852, #8DC26F);
  background: linear-gradient(to left, #76b852, #8DC26F);
  font-family: "Roboto", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
