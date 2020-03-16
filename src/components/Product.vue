<template>
  <div class="product">
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
    />
    <img :src="imageUrl" />
    <h1 class="link">
      <router-link :to="{ name: 'Product', params: { id } }">
        {{ name }}
      </router-link>
    </h1>
    <p>{{ description }}</p>
    <p>{{ price }}</p>
    <div class="buying-details">
      <div class="cart">
        <button :disabled="!availableProducts" @click="addToCart">
          Add to Cart
        </button>
        <h2 class="buy-banner" v-show="availableProducts">Buy now!</h2>
      </div>
      <div class="review">
        <template v-for="number in 5">
          <span
            :key="number"
            class="fa fa-star"
            :class="{ checked: number <= rating }"
          />
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    element: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    availableProducts() {
      return this.element.quantityAvailabe - this.inCartProducts;
    },
    description() {
      return this.element.description || "";
    },
    id() {
      return this.element.id || "";
    },
    imageUrl() {
      return this.element.imageUrl || "";
    },
    name() {
      return this.element.name || "";
    },
    price() {
      return `$${this.element.cost || 0}`;
    },
    rating() {
      return this.element.rating || 0;
    }
  },
  data() {
    return {
      inCartProducts: 0
    };
  },
  methods: {
    addToCart() {
      this.inCartProducts++;
    }
  }
};
</script>

<style scoped>
img {
  max-height: 200px;
  max-width: 200px;
}

.cart,
.buying-details {
  align-items: center;
  display: flex;
}

.buying-details {
  justify-content: space-between;
}

.link > a {
  color: inherit;
  text-decoration: none;
}

.buy-banner {
  margin-left: 10px;
}

.product {
  box-shadow: 0 0 5px 3px rgba(0, 0, 0, 0.25);
  margin: 10px;
  padding: 50px;
  text-align: left;
  width: 500px;
}

.checked {
  color: orange;
}
</style>
