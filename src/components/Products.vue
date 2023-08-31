<script setup>
import ProductItem from './ProductItem.vue';
import axios from 'axios'
import { MagnifyingGlassIcon } from '@heroicons/vue/24/solid'
import { onMounted, ref, computed } from 'vue';
// const products = [
//     {
// id: 1,
// name: 'Basic Tee',
// href: '#',
// imageSrc: 'https://tailwindui.com/img/ecommerce-images/product-page-01-related-product-01.jpg',
// imageAlt: "Front of men's Basic Tee in black.",
// price: '$35',
// color: 'Black',
//     },
// ]

const products = ref([]);
const categories = ref([]);
const orderby = ref(['ASC'])
const search = ref('')
const selected_categories = ref([])
const min = ref(0)
const max = ref(1000)

onMounted(() => {
    axios.get('https://dummyjson.com/products')
        .then(res => {
            products.value = res.data.products
            //    console.log(res.data);
        })

    axios.get('https://dummyjson.com/products/categories')
        .then(res => {
            categories.value = res.data
            // console.log(res.data);
        })
})

const filteredProduct = computed(() => {
    let result = products.value;
    if (search.value.length > 0) {
        result = products.value.filter(e => {
            return e.title.toLowerCase().includes(search.value.toLowerCase())
        });
    } 

    if (orderby.value === 'DESC') {
        result.sort((a, b) => b.id - a.id)
    } 

    if(selected_categories.value.length > 0){
        result = products.value.filter(e => {
            return selected_categories.value.includes(e.category)
        });
    }

    if(min.value > 0){
        result = result.filter(e => e.price > min.value)
    }

    if(max.value > 1000){
        result = result.filter(e => e.price > max.value)
    }

    return result;
});

</script>

<template>
    <div class="bg-white flex py-16 sm:py-24">
        <div class="w-2/12 px-6">
            <h2 class="text-xl font-bold tracking-tight text-gray-900">
                Filter By Category
            </h2>
            <ul class="mt-4">
                <li v-for="(category, index) in categories" :key="index">
                    <label for="check">
                        <input v-model="selected_categories" :value="category" type="checkbox" id="check">
                        {{ category }}
                    </label>
                </li>
            </ul>
            <hr class="mt-5 mb-2">
            <h2 class="text-xl font-bold tracking-tight text-gray-900">
                Filter By Price
            </h2>
            <div>
                <div class="flex justify-between">
                    <label for="default-range" class="block mb-2 text-sm font-medium text-gray-800 dark:text-white">
                        Min
                    </label>
                    <span>{{ min }}</span>
                </div>
                <input type="range" v-model="min" id="default-range" max="1000"
                    class="w-full h-2 bg-gray-700 rounded-lg appearance-none cursor-pointer dark:bg-gray-600">
                <!-- ----------------------------------- -->
                <div class="flex justify-between">
                    <label for="default-range" class="block mb-2 text-sm font-medium text-gray-800 dark:text-white">
                        Max
                    </label>
                    <span>{{ max }}</span>
                </div>
                <input type="range" v-model="max" id="default-range" max="10000"
                    class="w-full h-2 bg-gray-700 rounded-lg appearance-none cursor-pointer dark:bg-gray-600">


            </div>
        </div>

        <div class="w-10/12">
            <div class="mx-auto max-w-2xl px-4 sm:px-6 lg:max-w-7xl lg:px-8">

                <div class="flex justify-between">
                    <div class="search-div w-1/2 relative">
                        <input v-model="search" type="text"
                            class="border border-t-gray-300 px-4 py-3 w-full rounded outline-none">
                        <MagnifyingGlassIcon class="w-6 absolute top-3 right-2 text-gray-600" />
                    </div>

                    <select v-model="orderby" class="border border-t-gray-300 px-3 py-3 rounded">
                        <option value="ASC">ASC</option>
                        <option value="DESC">DESC </option>
                    </select>
                </div>
                <div class="mt-6 grid grid-cols-1 gap-x-6 gap-y-10 sm:grid-cols-2 lg:grid-cols-4 xl:gap-x-8">
                    <ProductItem v-for="product in filteredProduct" :key="product.id" :product="product" />
                </div>
            </div>
        </div>
    </div>
</template>



<style lang="scss" scoped></style> 