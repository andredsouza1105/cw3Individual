<script setup>
import productList from "./components/productList.vue"
import checkout from "./components/checkout.vue"
</script>

<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <h2> My name is Andre</h2>
      <input type="text" v-model="searchValue"> <br><br>
      <p>
                    <strong>Sort By:</strong>
                    <select v-model="sort">
                        <option disabled value="">Sort Options</option>
                        <option v-for="(option,key) in sort_options" v-bind:value="option">{{option}}</option>
                    </select>
                </p>

      <button @click="showCheckout">{{ this.cart.length }} Checkout</button>
    </header>
    <br>
    <main>
      <div v-if="currentView">
        <productList :sort="sort" :searchValue="searchValue" :lessons="lessons" :cart="cart" @addProduct="addToCart"></productList>
      </div>
      <div v-else>
        <checkout :lessons="lessons" :cart="cart" @removeProduct="removeOne"></checkout>
      </div>
    </main>
  </div>
</template>


<script>
export default {
  name: 'app',
  data() {
    return {
      sitename: "Pet Store App",
      cart: [],
      currentView: true,
      lessons: [],
      cart: [],
      sort_options: {
                        location: "Location",
                        location_desc: "Location Descending",
                        price: "Price",
                        price_desc: "Price Descending",
                        subject: "Subject",
                        subject_desc: "Subject Descending",
                        availaibility: "Avaialability",
                        availaibility_desc: "Availability Descending"
                    },
        searchValue:"",
        sort:"Price"
    }
  },
  components: { productList, checkout },
  mounted: function () {
    fetch("http://localhost:3000/collection/lessons")
      .then(response => response.json())
      .then(json => {
        this.lessons = json;

      })

  },
  methods: {
    removeOne(id) {
      let check = true;
      for (let i = 0; i < this.cart.length; i++) {
        if (check == true) {
          if (id == this.cart[i]) {
            this.cart.splice(i, 1);
            check = false;
          }
        }

        if (this.cart.length == 0) {
          this.showLesson = true;
        }
      }

    },

    showCheckout() {
      this.currentView = this.currentView ? false : true;
    },
    addToCart(lesson) {
      this.cart.push(lesson.id);
      console.log(this.cart)
    }
  },
  computed: {

  }
}
</script>

<style scoped></style>
