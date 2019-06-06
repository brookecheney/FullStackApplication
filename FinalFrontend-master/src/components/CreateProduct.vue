<template>
  <section class="productSection">
    <h1 class="title is-4">Create Product</h1>
    <b-field label>
      <b-input v-model="name" placeholder="Name"></b-input>
    </b-field>

    <b-field label>
      <b-input v-model="country" placeholder="Country"></b-input>
    </b-field>

    <b-field label>
      <b-input v-model="price" placeholder="Price"></b-input>
    </b-field>

    <!-- <b-field label>
      <b-input v-model="id" placeholder="ID"></b-input>
    </b-field>-->

    <b-button is-danger @click="createProduct">Create Product</b-button>
  </section>
</template>

<script>
import { EventBus } from "@/eventBus.js";
import gql from "graphql-tag";

export default {
  data() {
    return {
      name: null,
      country: null,
      price: null,
      id: null
    };
  },
  methods: {
    createProduct() {
      this.$apollo
        .mutate({
          mutation: gql`
            mutation createProduct(
              $name: String
              $price: Int
              $country: String
            ) {
              createProduct(
                data: { name: $name, price: $price, country: $country }
              ) {
                name
                price
                country
              }
            }
          `,
          variables: {
            name: this.name,
            price: parseInt(this.price),
            country: this.country
          }
        })
        .then(res => {
          console.log(res);
          this.$notification.open({
            message: "Product Created",
            type: "is-success"
          });
          EventBus.$emit("displayProducts");
        })
        .catch(err => {
          this.error = err;
          this.$notification.open({
            message: this.error,
            type: "is-warning"
          });
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.productSection {
  padding: 20px;
  border: solid 1px rgb(243, 243, 243);
  border-radius: 5px;
}
</style>
