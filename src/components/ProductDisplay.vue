<template>
  <!-- <PageLoader /> -->
  <div
    class="product"
    v-if="
      products.category.includes('men') || products.category.includes('women')
    "
  >
    <div
      class="container"
      :class="{
        'men-latar': products.category.includes('men'),
        'women-latar': products.category.includes('women'),
      }"
    ></div>
    <div class="card" :key="products.id">
      <div class="image">
        <img :src="products.image" alt="" />
      </div>
      <div class="content">
        <h1
          :class="{
            'text-men': products.category.includes('men'),
            'text-women': products.category.includes('women'),
          }"
        >
          {{ products.title }}
        </h1>
        <div class="category">
          <p>{{ products.category }}</p>
          <div class="rating">
            <p>{{ products.rating.rate }}/5</p>
            <span
              v-for="value in ratings"
              :key="value"
              :class="{
                'border-men': products.category.includes('men'),
                'border-women': products.category.includes('women'),
                'bg-men':
                  value < products.rating.rate &&
                  products.category.includes('men'),
                'bg-women':
                  value < products.rating.rate &&
                  products.category.includes('women'),
              }"
            ></span>
          </div>
        </div>
        <div class="line"></div>
        <div class="description">
          <p>{{ products.description }}</p>
        </div>
        <div class="line"></div>
        <div
          class="price"
          :class="{
            'text-men': products.category.includes('men'),
            'text-women': products.category.includes('women'),
          }"
        >
          ${{ products.price }}
        </div>
        <div class="container-btn">
          <a
            class="btn"
            :class="{
              'bg-men text-white': products.category.includes('men'),
              'bg-women text-white': products.category.includes('women'),
            }"
            >Buy Now</a
          >
          <a
            class="btn"
            :class="{
              'border-men text-men': products.category.includes('men'),
              'border-women text-women': products.category.includes('women'),
            }"
            @click="getCatalog"
            >Next Product</a
          >
        </div>
      </div>
    </div>
  </div>
  <div class="product" v-else>
    <div class="container blank-latar"></div>
    <div class="card" :key="products.id">
      <div class="blank-img">
        <img src="../assets/img/sad-face.svg" alt="" />
        <p>This product is unavailable to show</p>
        <a class="blank-btn" @click="getCatalog">Next Product</a>
      </div>
    </div>
  </div>
</template>

<script>
// import PageLoader from "./components/PageLoader.vue";
import axios from "axios";
export default {
  data() {
    return {
      products: [],
      index: 0,
      ratings: [1, 2, 3, 4, 5],
    };
  },
  methods: {
    getCatalog() {
      this.index++;
      if (this.index > 20) {
        this.index = 1;
      }
      const url = `https://fakestoreapi.com/products/${this.index}`;
      axios.get(url).then((res) => {
        this.products = res.data;
        console.log(res.data);
      });
    },
  },

  mounted() {
    this.getCatalog();
  },
};
</script>

<style>
@import "../assets/css/display.css";
.product {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.men-latar {
  background-image: url(../assets/img/bg-pattern.png),
    url(../assets/img/man-bg.png);
  background-repeat: no-repeat;
  background-position: center top;
  background-size: cover;
  object-fit: cover;
}
.women-latar {
  background-image: url(../assets/img/bg-pattern.png),
    url(../assets/img/woman-bg.png);
  background-repeat: no-repeat;
  background-position: center top;
  background-size: cover;
  object-fit: cover;
}
.blank-latar {
  background-image: url(../assets/img/grey-bg.png);
  background-repeat: no-repeat;
  background-position: center top;
  background-size: cover;
  object-fit: cover;
}
</style>
