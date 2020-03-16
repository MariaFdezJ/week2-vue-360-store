<template>
  <div class="store">
    <template v-for="(element, idx) in elements.message.products">
      <Product :key="idx" :element="element" />
    </template>
  </div>
</template>

<script>
import Product from "./Product";
import fakeData from "../fakeData";

export default {
  components: {
    Product
  },
  data() {
    return {
      elements: {}
    };
  },
  created() {
    this.elements = fakeData;
  }
};
</script>

<style scoped>
.store {
  align-items: center;
  display: flex;
  flex-direction: column;
}
</style>
