<template>
    <div>
      <div id="nav">
        <router-link id="logo-url" to="/">
          <img id="logo" :src="logo" :alt="alt">
        </router-link>
        <div id="title"><h1>Drones Store</h1></div>
        <router-link to="/">Home</router-link>
        <router-link to="/emails">Emails Cadastrados</router-link>
      </div>
    </div>
  </template>
  
  <script>
  
  export default {

    name: "Navbar",
    props: ["logo", "alt"],
    data() {
      return {
        cart: 0,
      }
    },
    methods: {
    }
  }
  </script>
  
  <style scoped>
    #nav {
      background-color: #222;
      border-bottom: 4px solid #111;
      padding: 15px 50px;
      display: flex;
      justify-content: flex-end;
      align-items: center;
    }
  
    #nav #logo-url {
      margin: auto;
      margin-left: 0;
    }

    #title {
      margin: auto;
      margin-left: 70px;
    }
  
    #logo {
      width: 70px;
      height: 70px;
    }
  
    #nav a {
      color: #FFFe;
      text-decoration: none;
      margin: 12px;
      transition: .5s;
    }
  
    #nav a:hover {
      color: #FFF;
      font-weight: bold;
      text-decoration: underline;
    }

    h1 {
      font-size: 50px;
      color: #FFF;
      justify-content: center;
  }
  
  </style>