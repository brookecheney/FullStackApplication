<template>
  <div>
    <BoxContainer class="boxContainer">
      <span class="title" slot="title">Restful</span>
    </BoxContainer>
    <RestfulProducts v-if="displayProducts"></RestfulProducts>
    <CreateProduct v-if="displayCreate"></CreateProduct>
  </div>
</template>

<script>
import { EventBus } from "@/eventBus.js";
import BoxContainer from "@/components/BoxContainer.vue";
import RestfulProducts from "@/components/RestfulProducts.vue";
import CreateProduct from "@/components/CreateProduct.vue";
export default {
  components: { BoxContainer, RestfulProducts, CreateProduct },
  data() {
    return {
      displayProducts: true,
      displayCreate: false
    };
  },
  mounted() {
    EventBus.$on("displayCreateProduct", () => {
      this.displayProducts = false;
      this.displayCreate = true;
    });
    EventBus.$on("displayProducts", () => {
      this.displayProducts = true;
      this.displayCreate = false;
    });
  }
};
</script>

<style lang="scss" scoped></style>
