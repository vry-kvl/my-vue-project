<template>
    <div class="container">
        <div class="row row-cols-1 row-cols-md-4 g-4">
            <div class="col" v-for="product in products" :key="product.id">
                <div class="card">
                    <img :src="product.thumbnail" class="card-img-top img-thumbnail p-0 border-0" height="200" alt="">
                    <div class="card-body">
                        <h5 class="card-title">{{ product.title }} - {{ product.brand }}</h5>
                        <p class="card-text">{{ product.description }}</p>
                        <a href="#" class="btn btn-primary">Read More</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            products: null
        };
    },
    methods: {
        getlastItem(myArray) {
            return myArray[myArray.length - 1];
        },
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