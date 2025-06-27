<template>
  <div>
    <div class="main-container">
      <h1>IShop 🛒</h1>
      <button class="toggle-btn" @click="toggleCart">
        {{ IsCartVisible ? "Hide Cart" : "Show Cart" }}
      </button>

      <h2>Products</h2>
      <div v-for="product in products" :key="product.id" class="product">
        <div>{{ product.name }} -> ${{ product.price }}</div>
        <button class="add-btn" @click="addToCart(product)">Add to Cart</button>
      </div>
    </div>
    <div v-if="IsCartVisible" class="cart-sidebar">
      <h2>Cart 🛒</h2>
      <div v-if="cart.length === 0">Your cart is empty</div>
      <div v-for="(item, index) in cart" :key="item.id" class="cart-item">
        <div>{{ item.name }} x {{ item.quantity }}</div>
        <button class="remove-btn" @click="removeFromCart(index)">❌</button>
      </div>
      <h3>Total: ${{ totalPrice }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "shop",
  data() {
    return {
      IsCartVisible: false,
      products: [
        { id: 1, name: "Apple", price: 40 },
        { id: 2, name: "Bread", price: 10 },
        { id: 3, name: "Milk", price: 60 },
        { id: 4, name: "Eggs", price: 15 },
      ],
      cart: [],
    };
  },
  methods: {
    toggleCart() {
      this.IsCartVisible = !this.IsCartVisible;
    },
    addToCart(product) {
      const existing = this.cart.find((item) => item.id === product.id);
      if (existing) {
        existing.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
  },
  computed: {
    totalPrice() {
      return this.cart
        .reduce((sum, item) => sum + item.price * item.quantity, 0)
        .toFixed(2);
    },
  },
};
</script>

<style scoped>
.main-container {
  padding-right: 300px;
}
.product {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
}
.add-btn {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}
.toggle-btn {
  position: fixed;
  top: 20px;
  right: 320px;
  background-color: #007bff;
  color: white;
  padding: 10px 15px;
  border-radius: 4px;
  border: none;
  cursor: pointer;
}
.cart-sidebar {
  width: 300px;
  background-color: #444040;
  border-left: 1px solid #ccc;
  padding: 20px;
  position: fixed;
  right: 0;
  top: 0;
  height: 100vh;
  overflow-y: auto;
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.1);
}
.cart-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #7c3636;
  border-radius: 6px;
}
.remove-btn {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 5px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
