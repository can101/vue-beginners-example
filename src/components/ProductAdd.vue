<template>
  <div id="addForm">
    <form @submit.prevent="handleAdd">
      <div class="form-group mt-2">
        <label for="id">Id</label>
        <input type="text" v-model="product.id" class="form-control" id="id" />
      </div>
      <div class="form-group mt-2">
        <label for="categoryId">categoryId</label>
        <input
          type="text"
          v-model="product.categoryId"
          class="form-control"
          id="categoryId"
        />
      </div>
      <div class="form-group mt-2">
        <label for="productName">productName</label>
        <input
          type="text"
          v-model="product.productName"
          class="form-control"
          id="productName"
        />
      </div>
      <div class="form-group mt-2">
        <label for="quantityPerUnit">quantityPerUnit</label>
        <input
          type="text"
          v-model="product.quantityPerUnit"
          class="form-control"
          id="quantityPerUnit"
        />
      </div>
      <div class="form-group mt-2">
        <label for="unitPrice">unitPrice</label>
        <input
          type="text"
          v-model="product.unitPrice"
          class="form-control"
          id="unitPrice"
        />
      </div>
      <div class="form-group mt-2">
        <label for="unitsInStock">unitsInStock</label>
        <input
          type="text"
          v-model="product.unitsInStock"
          class="form-control"
          id="unitsInStock"
        />
      </div>
      <button type="submit" class="btn btn-outline-success mt-3">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "product-add",
  data() {
    return {
      product: {
        id: "",
        categoryId: "",
        productName: "",
        quantityPerUnit: "",
        unitPrice: "",
        unitsInStock: "",
      },
    };
  },
  methods: {
    handleAdd() {
      this.$emit("add:product", this.product);
    },
  },
};
</script>

<style scoped>
#addForm {
  margin: 100px;
}
</style>
