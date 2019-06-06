<template>
  <div class="productBox">
    <div class="productHeader">
      <div class="prodName">
        <slot name="productName"></slot>
        <slot name="productCountry"></slot>
      </div>
      <slot name="productPrice"></slot>
    </div>
    <slot name="productId"></slot>
    <div class="buttonsContainer">
      <a @click="deleteProduct()" class="button is-white is-small">Delete</a>
      <a class="button is-white is-small">Edit</a>
    </div>
  </div>
</template>

<script>
export default {
  props: ["productId"],
  methods: {},
  mounted() {}
};
</script>

<style lang="scss" scoped>
.productBox {
  background: #20fc8f;
  border: solid 1px rgb(243, 243, 243);
  padding: 10px;
  border-radius: 5px;
  transition: all 0.5s ease;
  display: grid;
  .productHeader {
    display: grid;
    grid-template-columns: 1fr auto;
    grid-gap: 10px;
    margin-bottom: 10px;
    p {
      font-weight: 800;
    }
  }
  .prodId {
    align-self: flex-end;
  }
  .buttonsContainer {
    margin-top: 10px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
  }
}
.productBox:hover {
  transform: scale(1.02);
  box-shadow: 0px 0px 32px -6px rgba(0, 0, 0, 0.19);
}
</style>
