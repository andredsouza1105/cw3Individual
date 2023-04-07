<template>
  <div>
    <div class="lesson" v-for='lesson in sortedLessons'>
      <h2 v-text="lesson.subject" style="text-align:center;"></h2><i v-bind:class="lesson.icon"></i>
      <hr>
      <p>Location: {{ lesson.location }}</p>
      <p>Price: {{ lesson.price }}</p>
      <p>Spaces: {{ lesson.spaces - cartCount(lesson.id) }}</p>
      <img v-bind:src="lesson.image" width="100" height="100 "> <br> <br>

      <button v-on:click="addProduct(lesson)" v-if="canAddToCart(lesson)">
        <i class="fa-solid fa-cart-shopping"></i>
        Add to Cart</button>
      <button disabled="disabled" v-else>Add to Cart</button> <br> <br>
      <span v-if="lesson.spaces === cartCount(lesson.id)">
        All Out!
      </span>
      <span v-else>Buy Now!</span>

    </div>
  </div>
</template>
<script>
export default {
  name: 'products',
  props: ['lessons', 'cart','searchValue','sort'],
  data() {
    return {

    }
  },
  methods: {
    addProduct(lesson) {
      this.$emit('addProduct', lesson)
    },
    canAddToCart(lesson) {
      return lesson.spaces > this.cartCount(lesson.id);
    },
    cartCount(id) {
      let count = 0;
      for (let i = 0; i < this.cart.length; i++) {
        if (this.cart[i] === id) {
          count++;
        }
      }
      return count;
    }
  },
  computed:{
    sortedLessons() {
                        if (this.searchValue != "" && this.searchValue){
                            let lessonsArray=this.lessons;
                            lessonsArray= lessonsArray.filter((item)=>{
                                return item.subject.toUpperCase().includes(this.searchValue.toUpperCase())||item.location.toUpperCase().includes(this.searchValue.toUpperCase());
                            })
                            return lessonsArray;
                        }
                        if (this.sort == "Price") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.price > b.price)
                                    return 1;
                                if (a.price < b.price)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare);
                        }

                        else if (this.sort == "Price Descending") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.price > b.price)
                                    return 1;
                                if (a.price < b.price)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare).reverse();


                        }

                        else if (this.sort == "Location") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.location > b.location)
                                    return 1;
                                if (a.location < b.location)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare);


                        }
                        else if (this.sort == "Location Descending") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.location > b.location)
                                    return 1;
                                if (a.location < b.location)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare).reverse();


                        }
                        else if (this.sort == "Subject") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.subject > b.subject)
                                    return 1;
                                if (a.subject < b.subject)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare);


                        }
                        else if (this.sort == "Subject Descending") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.subject > b.subject)
                                    return 1;
                                if (a.subject < b.subject)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare).reverse();


                        }
                        else if (this.sort == "Avaialability") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.spaces > b.spaces)
                                    return 1;
                                if (a.spaces < b.spaces)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare);


                        }
                        else if (this.sort == "Availability Descending") {
                            let lessonsArray = this.lessons.slice(0);
                            function compare(a, b) {
                                if (a.spaces > b.spaces)
                                    return 1;
                                if (a.spaces < b.spaces)
                                    return -1;
                                return 0;
                            }
                            return lessonsArray.sort(compare).reverse();


                        
  }
}}}
</script>

<style scoped>
.lesson {
  border-radius: 20px;
  border-style: solid;
  margin-left: 20px;
  margin-right: 50%;
  margin-bottom: 50px;
  padding-left: 20px;
}
</style>
