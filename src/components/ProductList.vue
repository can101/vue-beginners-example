<template>
  <div id="productList">
    <h3>Product List</h3>
    <p v-if="products.length == 0">Ürün listesi boş</p>
    <table v-else class="table">
      <thead>
        <th>Id</th>
        <th>Ürün Adı</th>
        <th>Kategori</th>
        <th>Açıklama</th>
        <th>Birim Fiyatı</th>
        <th>Stok Adedi</th>
        <th></th>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td v-if="updateId == product.id">
            <input
              type="text"
              v-model="product.id"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.id }}</td>
          <td v-if="updateId == product.id">
            <input
              type="text"
              v-model="product.productName"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.productName }}</td>
          <td v-if="updateId == product.id">
            <input
              type="text"
              v-model="product.categoryId"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.categoryId }}</td>
          <td v-if="updateId == product.id">
            <input
              type="text"
              v-model="product.quantityPerUnit"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.quantityPerUnit }}</td>
          <td v-if="updateId == product.id">
            <input
              type="text"
              v-model="product.unitPrice"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.unitPrice }}</td>
          <td v-if="updateId == product.id">
            <input
              type="text"
              v-model="product.unitsInStock"
              class="form-control"
              id="id"
            />
          </td>
          <td v-else>{{ product.unitsInStock }}</td>
          <td v-if="updateId !== product.id">
            <button
              class="btn btn-sm btn-primary"
              @click="handleUpdate(product)"
            >
              Update
            </button>
            <button
              class="btn btn-sm btn-danger"
              @click="handleDelete(product)"
            >
              Del
            </button>
          </td>
          <td v-else>
            <button class="btn btn-sm btn-success" @click="handleSave(product)">
              kaydet
            </button>
            <button class="btn btn-sm btn-secondary" @click="updateId = null">
              iptal
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "product-List",
  data() {
    return {
      updateId: null,
    };
  },
  props: {
    products: Array,
  },
  methods: {
    handleDelete(product) {
      this.$emit("delete:product", product);
    },
    handleUpdate(product) {
      this.updateId = product.id;
    },
    handleSave(product) {
      this.$emit("update:product", product);
      this.updateId = null;
    },
  },
};
</script>

<style scoped>
#productList {
  margin: 100px;
}
</style>
