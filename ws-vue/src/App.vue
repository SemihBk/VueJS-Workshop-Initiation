<script>
export default {
  data() {
    return {
      product: "Socks",
      description: "De belles chaussettes rouges.",
      image: "./src/assets/images/socks_green.jpg",
      url: "vuejs.org",
      onSale: true,
      details: ["50% coton", "30% wool", "20% polyester"],
      variants: [
        {
          id: 1,
          color: "green",
          image: "./src/assets/images/socks_green.jpg",
          quantity: 15,
        },
        {
          id: 2,
          color: "blue",
          image: "./src/assets/images/socks_blue.jpg",
          quantity: 0,
        },
      ],
      sizes: ["S", "M", "L", "XL"],
      cart: 0,
      brand: "Vue mastery",
      selectedVariant: 0,
    };
  },

  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateVariant(index) {
      this.selectedVariant = index;
    },
    removeToCart() {
      this.cart -= 1;
    },
  },

  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].image;
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity;
    },
    onSale() {
      if (this.onSale == true) {
        return this.brand + " " + this.product + " " + "is on sale";
      } else {
        return this.brand + " " + this.product + " " + "will be on sale soon";
      }
    },
  },
};
</script>

<template>
  <div class="nav-bar"></div>

  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <a :href="url" target="_blank"
          ><img v-bind:src="image" :class="{ outOfStockImg: !inStock }"
        /></a>
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p>{{ description }}</p>
        <p v-if="inStock">In stock</p>
        <p v-else>Out of stock</p>
        <p>{{ onSale }}</p>
        <div class="list">
          <ul>
            <li v-for="detail in details">
              {{ detail }}
            </li>
          </ul>
          <ul>
            <li v-for="size in sizes">
              {{ size }}
            </li>
          </ul>
        </div>
        <div class="circle__container">
          <div
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
            v-for="(variant, index) in variants"
            :key="variant.id"
            @mouseover="updateVariant(index)"
          ></div>
        </div>
        <div class="button__container">
          <button
            class="button"
            @:click="addToCart"
            :class="{ disabledButton: !inStock }"
            :disabled="!inStock"
          >
            Add to cart
          </button>
          <button
            class="button"
            @:click="removeToCart"
            :class="{ disabledButton: cart == 0 }"
            :disabled="cart == 0"
          >
            Remove from cart
          </button>
        </div>
      </div>
      <div class="cart">Cart ({{ cart }})</div>
    </div>
  </div>
</template>
