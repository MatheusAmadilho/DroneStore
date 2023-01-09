<template>
    <div class="cart">
     <div @add="updateCart()"><img class="imgicon" src="https://cdn-icons-png.flaticon.com/512/60/60992.png">({{ cart }})</div>
    </div>
   `<div class="product-display container my-4">
     <div class="product-container row">
       <div class="product-image col-lg-5">
         <div class=picture>
           <img :src="activePic">
         </div>
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
           @click='updateCart()'>
           Buy
         </button>
         <div>
           <button type="button" class="outbutton btn col-lg-6" @click="showEmail" v-show="!inStock">Notify me when available</button>
         </div>
       </div>
       <div class="emailform col-md-3" v-show="mostrar_email, !inStock">
         <form id="email-form" method="POST" @submit="createEmail">
           <div class="input-container">
             <label for="email">We will notify you when this item will be available again in our stock!</label>
             <input v-if="validated" style="background-color :#00FA9A;" type="email" id="email" name="email" v-model="email" placeholder="Give your email">
             <input v-else style="background-color :	#FFF;" type="email" id="email" name="email" v-model="email" placeholder="Give your email">
           </div>
           <div class="input-container">
             <input class="regbutton submit-btn" type="submit" :class="{ disabledButton: !validated }" :disabled="!validated"  @click="showGreat(); showEmail();" value="Register my email!">
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
         <div class='pictures'>
            <div v-for="(picture, index) in pictures">
              <img :src="picture" @mouseover="changeActivePic(index)">
           </div>
         </div>
       </div>
     </div>
   </div>

</template>
<script>
   export default {
     name: "Phantom",
 
     data() {
     return {
         email: null,
         cart: 0,
         mostrar_great: false,
         mostrar_email: false,
         product: 'Phantom',
         brand: 'DJI',
         selectedVariant: 0,
         details: ["4K HDR Video",
        "Mechanical Shutter",
        "Obstacle sensing in five directions",
        "10km max transmission range"],
         variants: [
           { quantity: 0 },
         ],
         activePic: "/img/pic7.jpeg",
         pictures: [
           "/img/pic7.jpeg", 
           "/img/pic8.jpeg", 
           "/img/pic9.jpeg"
         ],

     }
   },
   methods: {
       updateCart() {
           this.$emit('add')
           this.cart +=1
       },
       changeActivePic(index) {
         this.activePic = this.pictures[index]
       },
       showEmail() {
           this.mostrar_email = !this.mostrar_email
       },
       showGreat() {
           this.mostrar_great = !this.mostrar_great
       },
       validateEmail(email) {
         const re = /^[\w.\+]+@\w+.\w{2,}(?:.\w{2})?$/; 
         return re.test(email);
       },
       async createEmail(e) {

         e.preventDefault()

         const data = {
           email: this.email
         }

         const dataJson = JSON.stringify(data)    

         const req = await fetch("http://localhost:3000/emails", {
           method: "POST",
           headers: { "Content-Type" : "application/json" },
           body: dataJson
         });

         const res = await req.json()

         this.email = ""

         }
   },
   computed: {
       title() {
           return this.brand + ' ' + this.product
       },
       inStock() {
           return this.variants[this.selectedVariant].quantity
       },
       validated(){
         return this.validateEmail(this.email)
       }
   }
}
</script>

<style scoped>

 .picture img{
   border: 2px solid #d8d8d8;
   width: 70%;
   margin: 40px;
   padding: 15px;
     -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
     -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
   box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
 }
 .pictures img{
   width: 80px;
   height: 80px;
   border: 2px solid #d8d8d8;
   margin: 10px;

 }
 .pictures{
   display: flex;
 }
  
 .imgicon{
   margin: auto;
 }
 
 .cart {
     margin-left: 91%;
     margin-top: 10px;
     margin-right: 2px;
     border: solid 1px #222;
     border-radius: 10px;
     width: 65px;
     height: 40px;
     padding: 5px;
     box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
       inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
       inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
     
   }
 .cart img {
   width: 30px;
   height: 30px;
   border: none;
   padding: 0;
   }

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

 #email-form {
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

 input {
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

 @media only screen and (max-width: 600px) {
 
 }
</style>