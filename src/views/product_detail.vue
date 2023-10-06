<template>
    <div>
      <h1>รายการสินค้า</h1>
      <div class="product-list">
        <div class="product-card" v-for="product in products" :key="product.id">
          <img :src="product.image" :alt="product.name">
          <h2>{{ product.name }}</h2>
          <p>{{ product.description }}</p>
          <p>ราคา: ฿{{ product.price }}</p>
          <p>จำนวน: {{ product.quantity }}</p>
          <button @click="addToCart(product)">เพิ่มลงในตะกร้า</button>
          <button @click="removeFromCart(product)">ลดจำนวน</button>
        </div>
      </div>
      <h2>ราคารวมในตะกร้า: ฿{{ calculateTotal() }}</h2>
    </div>

    
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [],
        cart: [], 
      };
    },
    created() {
      
      for (let i = 1; i <= 10; i++) {
        this.products.push({
          id: i,
          name: `สินค้าที่ ${i}`,
          description: `รายละเอียดสินค้าที่ ${i}`,
          price: (i * 10).toFixed(2),
          image: `url_to_image_${i}.jpg`,
          quantity: 0, 
        });
      }
    },
    methods: {
      addToCart(product) {
        
        product.quantity++;
      },
      removeFromCart(product) {
       
        if (product.quantity > 0) {
          product.quantity--;
        }
      },
      calculateTotal() {
        
        return this.cart.reduce((total, product) => total + product.price * product.quantity, 0);
      },
    },
  };
  </script>
  
  <style scoped>
 
  .product-list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  .product-card {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px;
    width: 200px;
    text-align: center;
  }

  
  </style>
  