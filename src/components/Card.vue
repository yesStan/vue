<template>
  <div id="app">
    <div class="product">
      <h1>{{ msg }}</h1>

            <div class="product-image">
                <img :src="image">
            </div>

            <div class="product-info">
                <h1>{{ title }}</h1>
                <p>{{ sale }}</p>
                <p v-if="inStock">In Stock</p>
                <p v-else class="outOfStock">Out of Stock</p>
                
                <ul>
                    <!-- <li v-for="(detail, index) in details">
                        {{ transformValue(index, details) }}
                    </li> -->
                    <li v-for="detail in details" v-bind:key="detail">
                        {{ detail }}
                    </li>
                <!-- тз v-for отобразить, в строчном виде все свойства и значения объектов,
                     'массиваVariants', в каждом спане отобразить свойства и ключи. -->
                </ul>
                <div class="color-box"
                    v-for="(variant, index) in variants"
                    :key="variant.variantId"
                    :style="{ backgroundColor: variant.variantColor }"
                    @mouseover="updateProduct(index)">
                </div>
                <ul v-for="size in sizes" :key="size">
                    <li>{{ size }}</li>
                </ul>
                <div class="button">
                    <button v-on:click="addToCart" 
                    :disabled="!inStock"
                    :class="{ disabledButton: !inStock }"
                    >Add to Cart</button>
                    <button v-on:click="deleteFromCart">Remove item</button>
                    <div class="cart">
                    <p>Cart ({{ cart }})</p>
                </div>
                </div>
                
            </div>
        </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    msg: String
  },
  data() {
    return {
        product: 'Socks',
        brand: 'Vue Mastery',
        selectedVariant: 0,
        details: ['80% cotton', '20% polyester', 'Gender-neutral'],
        sizes: [ 's', 'm', 'l', 'xl', 'xxl'],
        
        variants: [
          {
            variantId: 2234,
            variantColor: 'green',
            variantImage: 'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
            variantQuantity: 10     
          },
          {
            variantId: 2235,
            variantColor: 'blue',
            variantImage: 'https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg',
            variantQuantity: 0     
          }
        ],
        cart: 0,
        onSale: true
    }
  },
  methods: {
    addToCart: function() {
            this.cart += 1
        },
        updateProduct: function(index) {  
            this.selectedVariant = index
        },
        deleteFromCart: function () { 
            this.cart-- 
            if (this.cart <= 0) 
            { this.cart = 0 } 
        } 
  },
  computed: {
        title() {
            return this.brand + ' ' + this.product  
        },
        image(){
            return this.variants[this.selectedVariant].variantImage
        },
        inStock(){
            return this.variants[this.selectedVariant].variantQuantity
        },
        sale() {
          if (this.onSale) {
            return this.brand + ' ' + this.product + ' are on sale!'
          } 
            return  this.brand + ' ' + this.product + ' are not on sale'
        }
    }
}
</script>


<style scoped>
body {

    font-family: tahoma;
    color:#282828;
    margin: 0px;
  }
  
  /* .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  } */

  .product {
    /* display: flex;
    flex-flow: wrap;  */
 padding: 1rem;
  }
.outOfStock {
    text-decoration: line-through;
}
  img {
    border: 1px solid #d8d8d8;
    width: 50%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }
  
  /* .product-image {
    width: 80%;
  } */
  
  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }
  
  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }
  .button {
    display: flex;
    justify-content: space-evenly;
    align-items: baseline;
    padding: 10px;
  }
  
  .cart {
    margin-right: 25px;
    float: left;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  } 
  
  .disabledButton {
    background-color: #d8d8d8;
  }
  
  /* .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
  } */
  
  input {
    width: 100%;  
    height: 25px;
    margin-bottom: 20px;
  }
  
  textarea {
    width: 100%;
    height: 60px;
  }

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
 /* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}  */

</style>
