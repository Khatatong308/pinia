<template>
  <h1 class="mt-3">ตะกร้าสินค้า</h1>
  <div class="d-flex justify-content-center" v-if="!product_store.load_products">
      <h2>กำลังโหลดข้อมูลสินค้า...</h2>
  </div>
  <table class="table" v-else>
      <thead>
          <tr>
              <th>สินค้า</th>
              <th>ราคา</th>
              <th>จำนวน</th>
              <th>รวม</th>
              <th>ลบสินค้า</th>
          </tr>
      </thead>
      <tbody>
          <tr v-for="(cart, index) in carts" :key="index">
              <td>
             </td>
          </tr>
      </tbody>
  </table>
      <button class="btn btn-primary mb-5" @click="cart_store.clear_cart()">เคลียตะกร้า</button>
      <button class="btn btn-success mb-5 mx-2">รวม {{ currencyTHB(cart_store.total) }}</button>
 </template>

<script setup>
import { computed } from 'vue'
import { currencyTHB } from '../shared/currency'
import { useProductStore } from '../store/product'
import { useCartStore } from '../store/cart';
const product_store = useProductStore()
const cart_store = useCartStore()
const carts = computed(() => cart_store.cart_previews)

</script>
<style lang="scss" scoped>
</style>