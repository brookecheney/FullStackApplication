<template>
  <div>
    <BoxContainer class="boxContainer">
      <span class="title" slot="title">GraphQL</span>
    </BoxContainer>
    <GraphQlProducts v-if="displayProducts"></GraphQlProducts>
    <CreateProduct v-if="displayCreate"></CreateProduct>
  </div>
</template>

<script>
import { EventBus } from "@/eventBus.js";

import BoxContainer from "@/components/BoxContainer.vue";
import GraphQlProducts from "@/components/GraphQlProducts.vue";
import CreateProduct from "@/components/CreateProduct.vue";
export default {
  components: { BoxContainer, GraphQlProducts, CreateProduct },
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

<style lang="scss" scoped>
.boxContainer {
  h1 {
    color: #167df3;
  }
}
</style>
