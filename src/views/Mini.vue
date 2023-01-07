<template>
    `<div class="product-display container my-4">
      <div class="product-container row">
        <div class="product-image col-lg-5">
          <img v-bind:src="image">
        </div>

        <div class="product-info col-md-4">
          <h1>{{ title }}</h1>
          
          <ul>
            <li v-for="detail in details">{{ detail }}</li>
          </ul>

          <div class="buttonstock">
            <p v-if="inStock" style="background-color :#23e16b;border-radius: 10px;font-size: 20px;">In Stock</p>
            <p v-else style="background-color :#d94d65;border-radius: 10px;font-size: 20px;">Out of Stock</p>
          </div>
      
          <button 
            class="button" 
            :class="{ disabledButton: !inStock }" 
            :disabled="!inStock" 
            @click="$emit('updateCart')">
            Buy
          </button>
          <div>
            <button type="button" class="outbutton btn col-lg-6" @click="showEmail" v-show="!inStock">Notify me when available</button>
          </div>
        </div>
        <div class="emailform col-md-3" v-show="mostrar_email, !inStock">
          <form id="burger-form">
            <div class="input-container">
              <label for="nome">We will notify you when this item will be available again in our stock!</label>
              <input type="email" id="email" name="email" v-model="email" placeholder="Give your email">
            </div>
            <div class="input-container">
              <button class="regbutton" @click.prevent="showGreat(); showEmail();">Register my email!</button>
              <button class="canbutton" @click.prevent="showEmail">Cancel</button>
            </div>
          </form>
        </div>
        <div class="emailmsg col-md-3" v-show="mostrar_great">
            <label for="name">Great!</label>
            <label for="name">Your email has been registered!</label>
            <button type="button" class="canbutton" @click="showGreat">Close</button>
        </div>
        <div class="gallery row">
          <div
            v-for="(variant, index) in variants" 
            :key="variant.image" 
            @mouseover="updateVariant(index)" 
            class="color-circle col-lg-6" 
            :style="{ backgroundImage: variant.image }" >
          </div>
        </div>
      </div>
    </div>

</template>
<script>
    export default {
      name: "Mini",
      emits: ['updateCart'],
      data() {
      return {
          mostrar_great: false,
          mostrar_email: false,
          product: 'Mini 3',
          brand: 'DJI',
          selectedVariant: 0,
          details: ["Under 249 g","4K HDR Video","38kph (level 5) wind resistance","10km max transmission range"],
          variants: [
            { id: 2234, image: "/img/pic1.jpeg", quantity: 1 },
            { id: 2234, image: "/img/pic2.jpeg", quantity: 0 },
            { id: 2234, image: "/img/pic3.jpeg", quantity: 0 },
          ],
      }
    },
    methods: {
        updateVariant(index) {
            this.selectedVariant = index
        },
        showEmail() {
            this.mostrar_email = !this.mostrar_email
        },
        showGreat() {
            this.mostrar_great = !this.mostrar_great
        }
    },
    computed: {
        title() {
            return this.brand + ' ' + this.product
        },
        image() {
            return this.variants[this.selectedVariant].image
        },
        inStock() {
            return this.variants[this.selectedVariant].quantity
        },
    }
}
</script>

<style scoped>

 .emailmsg{
  max-width: 400px;
  border: 2px solid #d8d8d8;
  padding: 10px;
  width: 250px;
  height: 170px;
 }

 .canbutton{
  border: none;
  text-decoration: underline;
  color: #39495c;
  margin-left: 80px;
 }
 .canbutton:hover{
  font-weight: bold;
 }
 .regbutton {
    margin-bottom: 1px;
    background-color: #39495c;
    border-radius: 5px;
    font-size: 18px;
    width: 200px;
    height: 40px;
    color: #FFF;
    box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
        inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
        inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
    text-align: center;
    cursor: pointer;
 }
 .regbutton:hover{
  background-color: #fff;
  color: #39495c;
  border: solid 2px #222;
}

 .outbutton{
    margin: 30px;
    margin-bottom: 1px;
    background-color: #39495c;
    border-radius: 5px;
    font-size: 18px;
    width: 250px;
    height: 40px;
    color: #FFF;
    box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
        inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
        inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
    text-align: center;
    cursor: pointer;
 }

 .outbutton:hover{
  background-color: #fff;
  color: #39495c;
  border: solid 2px #222;
}
 .emailform {
  padding: 50px;

 }

#burger-form {
    max-width: 400px;
    border: 2px solid #d8d8d8;
    padding: 10px;
    width: 400px;
  }

  .input-container {
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    color: #222;;
    padding: 5px 10px;
    
  }

  input, select {
    padding: 5px 10px;
  }


.button {
  margin: 30px;
  background-color: #39495c;
  border-radius: 5px;
  font-size: 20px;
  width: 90px;
  height: 60px;
  color: white;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
  margin-top: 15px;
}

.button:hover{
  background-color: #fff;
  color: #39495c;
}

.buttonstock{
  margin: 30px;
  font-size: 10px;
  width: 150px;
  height: 30px;
  color: white;
  text-align: center;
}

.color-circle {
  width: 60px;
  height: 60px;
  border: 2px solid #d8d8d8;
  margin: 10px;
}

.gallery{
  margin-top: 0%;
  margin-left: 50px;
}


.disabledButton {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

h1 {
  width: 250px;
  font-size: 50px;
  margin-right: 500px;
}

h3 {
  font-size: 25px;
}

img {
  border: 2px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  padding: 15px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
}

label {
  font-size: 20px;
  margin-bottom: 5px;
}

li {
  font-size: 18px;
}

.out-of-stock-img {
  opacity: 0.5;
}

p {
  font-size: 22px;
}

select {
  height: 40px;
  font-size: 20px;
  background-color: white;
  cursor: pointer;
}

textarea {
  width: 95%;
  height: 70px;
  padding: 10px;
  font-size: 20px;
  margin-bottom: 20px;
}

@media only screen and (max-width: 600px) {
 

}
</style>