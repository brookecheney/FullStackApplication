<template>
  <div class="productsContainer">
    <ProductCard
      v-for="product in products"
      :key="product.id"
      class="productBox"
    >
      <h1 slot="productName" class="title is-6">{{ product.name }}</h1>
      <h1 slot="productCountry" class="subtitle is-7">{{ product.country }}</h1>
      <p slot="productPrice" class="title is-5">${{ product.price }}</p>
      <p slot="productId" class="prodId is-size-7 has-text-grey">
        ID: {{ product.id }}
      </p>
    </ProductCard>
  </div>
</template>

<script>
import ProductCard from "@/components/ProductCard.vue";
import gql from "graphql-tag";
export default {
  components: { ProductCard },
  data() {
    return {
      products: []
    };
  },
  apollo: {
    products: gql`
      query {
        products {
          id
          name
          price
          country
        }
      }
    `
  }
};
</script>

<style lang="scss" scoped>
.productsContainer {
  display: grid;
  grid-gap: 20px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}
</style>
