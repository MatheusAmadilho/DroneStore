<template>
    <div>
      <div id="nav">
        <router-link id="logo-url" to="/">
          <img id="logo" :src="logo" :alt="alt">
        </router-link>
        <div id="title"><h1>Drones Store</h1></div>
        <router-link to="/">Home</router-link>
        <router-link to="/emails">Emails Cadastrados</router-link>
        <div @add-to-cart="updateCart" class="cart">Cart({{ cart }})</div>
      </div>
    </div>
  </template>
  
  <script>
  
  export default {
    name: "Navbar",
    props: ["logo", "alt"],
    data() {
      return {
          cart: [],
      }
    },
    methods: {
      updateCart() {
            this.cart +=1
        }
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

    #nav #title {
      margin: auto;
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
    .cart {
      color: #FFF;
      margin: 25px 100px;
      float: right;
      border: 1px solid #d8d8d8;
      padding: 10px 30px;
      -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
      -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
      box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
    }

    h1 {
      font-size: 50px;
      color: #FFF;
      justify-content: center;
  }
    .title{
      justify-content: center;
    }
  </style>