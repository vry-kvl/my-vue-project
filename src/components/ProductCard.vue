<style>
@import '@/assets/css/ProductCard.css';
</style>
<template>
    <div class="container">
        <div class="row row-cols-1 row-cols-md-4 g-4">
            <div class="col d-flex align-items-stretch" v-for="product in products" :key="product.id">
                <div class="card">
                    <img :src="product.thumbnail" class="card-img-top p-0 border-0 object-fit-cover" height="200" alt="">
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title">{{ product.title }} - {{ product.brand }}</h5>
                        <p class="card-text">{{ product.description }}</p>
                        <a href="#" @click.prevent="fadeMe(product)" class="btn btn-primary mt-auto align-self-start w-100">Add
                            to cart</a>
                    </div>
                </div>
            </div>
        </div>
        <Transition @enter="fadeAlert">
            <div v-if="show" class="message-wrapper position-fixed top-0 mt-4 start-0 w-100">
                <div class="alert alert-success w-75 mx-auto" role="alert">
                    <b>{{ addedProductTitle }}</b> is successfully added!
                </div>
            </div>
        </Transition>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            products: null,
            show: false,
            addedProductTitle: null
        };
    },
    methods: {
        fadeMe: function (product) {
            this.show = !this.show
            this.addedProductTitle = product.title.concat(' - ').concat(product.brand);
        },
        fadeAlert() {
            var that = this;
            setTimeout(function () {
                that.show = false;
            }, 2000);
        }
    },
    mounted() {
        axios.get('https://dummyjson.com/products')
            .then(response => {
                this.products = response.data.products;
            })
            .catch(error => {
                console.error(error);
            });
    }
}
</script>