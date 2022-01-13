<template>
  <div id="app">
    <ProductAdd @add:product="addProduct" />
    <ProductList
      @delete:product="deleteProduct"
      @update:product="updateProduct"
      :products="products"
    />
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import ProductAdd from "./components/ProductAdd.vue";

export default {
  name: "App",
  components: {
    ProductList,
    ProductAdd,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    this.getProducts();
  },
  methods: {
    async getProducts() {
      const res = await fetch("http://localhost:3000/products");
      const data = await res.json();
      this.products = data;
    },
    async deleteProduct(product) {
      await fetch("http://localhost:3000/products/" + product.id, {
        method: "DELETE",
        headers: { "Content-Type": "application/json" },
      });
      this.products = this.products.filter(
        (productToFilter) => productToFilter.id !== product.id
      );
    },
    async addProduct(product) {
      const res = await fetch("http://localhost:3000/products", {
        method: "POST",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });
      const newProduct = await res.json();
      this.products = [...this.products, newProduct];
    },
    async updateProduct(product) {
      const res = await fetch("http://localhost:3000/products/" + product.id, {
        method: "PUT",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });
      const updatedProduct = res.json();
      this.products = this.products.map((item) =>
        item.id == updatedProduct.id ? updatedProduct : item
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
