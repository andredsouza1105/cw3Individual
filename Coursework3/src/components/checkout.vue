<template>
    <div>
        <h1> Welcome to Checkout</h1>
        <div v-for='lesson in lessons'>
            <div class="lesson" v-if="cartCount(lesson.id) > 0">
                <h2 v-text="lesson.subject" style="text-align:center;"></h2><i v-bind:class="lesson.icon"></i>
                <hr>
                <p>Location: {{ lesson.location }}</p>
                <p>Price: {{ lesson.price }}</p>
                <p>Amount: {{ cartCount(lesson.id) }}</p> 

                


                <img v-bind:src="lesson.image" width="100" height="100 ">
                <br>
                <button @click="removeProduct(lesson)">Remove One</button>
                <br><br>

            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'checkout',
    props: ['lessons', 'cart'],
    data() {
        return {

        }
    },
    methods: {
        cartCount(id) {
            let count = 0;
            for (let i = 0; i < this.cart.length; i++) {
                if (this.cart[i] === id) {
                    count++;
                }
            }
            return count;
        },
        removeProduct(product) { 
            this.$emit('removeProduct',product.id)
        }
    }
}
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
