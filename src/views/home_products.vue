<template>
  <div>
    <h1>รายการสินค้า</h1>
    <div class="product-list">
      <div class="product-card" v-for="product in products" :key="product.id">
        <img :src="product.image" :alt="product.name">
        <h2>{{ product.name }}</h2>
        <p>{{ product.description }}</p>
        <p>ราคา: ฿{{ product.price }}</p>
        <div>
          <button @click="addToCart(product)">เพิ่มลงในตะกร้า</button>
          <button @click="removeFromCart(product)" :disabled="product.cartQuantity === 0">ลดจากตะกร้า</button>
          <p>ผลรวม: ฿{{ total }}</p>
          <span>{{ product.cartQuantity }}</span>
          </div>
      </div>
    </div>
  </div>
  
</template>


<script>
export default {
  data() {
    return {
      products: [],
      total: 0, 
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
        cartQuantity: 0, 
      });
    }
  },
  methods: {
    addToCart(product) {
      product.cartQuantity++;
      this.calculateTotal(); 
    },
    removeFromCart(product) {
      if (product.cartQuantity > 0) {
        product.cartQuantity--;
        this.calculateTotal(); 
      }
    },
    calculateTotal() {
  this.total = this.products.reduce((total, product) => {
    if (product.cartQuantity > 0) {
      return total + product.price * product.cartQuantity;
    }
  return total;
      }, 
    0);
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

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
