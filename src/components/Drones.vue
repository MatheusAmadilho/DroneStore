<template>
    <div>
      <div id="nav">
        <button class="button"><router-link to="/mini">DJI Mini 3</router-link></button>
        <button class="button"><router-link to="/Products02">DJI Phantom</router-link></button>
        <button class="button"><router-link to="/Products03">DJI Avata</router-link></button>
      </div>
    </div>
    <div class="product-image">
        <img src="/img/pic1.jpeg">
        <img src="/img/pic7.jpeg">
        <img src="/img/pic13.jpeg">
    </div>
  </template>
  
  <script>
  
  export default {
    name: "Drones",
      data() {
      return {
        
      }
    },
    methods: {
    
    },
}
  </script>
  
  <style scoped>
    #nav {
      background-color: #FFF;
      padding: 15px 50px;
      display: flex;
      justify-content: space-around;
      align-items: center;
    }
  
    #nav a {
      color: #FFF;
      text-decoration: none;
      margin: 12px;
      transition: .5s;
    }
  
    #nav a:hover {
      color: #FFF;
      font-weight: bold;
      text-decoration: underline;
    }

    .button {
    margin: 30px;
    margin-bottom: 1px;
    background-color: #39495c;
    border-radius: 5px;
    font-size: 18px;
    width: 180px;
    height: 70px;
    color: #FFF;
    padding: 20px;
    box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
        inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
        inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
    text-align: center;
    cursor: pointer;
    }

    img {
    border: 2px solid #d8d8d8;
    width: 28%;
    margin: 41px;
    padding: 15px;
    -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
    -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
    box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
    }

    @media only screen and (max-width: 600px) {
    
    }
  </style>