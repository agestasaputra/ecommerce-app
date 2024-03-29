<template>
  <div class="min-h-[100vh] h-full bg-white">
    <!-- Nav -->
    <nav class="flex flex-row justify-between items-center py-3 px-4 bg-blue-500">
      <NuxtLink :to="'/'" class="text-white hover:text-blue-500">
        <ArrowLeftIcon class="h-6 w-6" />
      </NuxtLink>
      <h1 class="font-semibold text-[16px] text-white mb-1">
        Product
      </h1>
      <div class="flex flex-row">
        <button class="text-white hover:text-blue-950 mr-2">
          <BellIcon class="h-6 w-6" />
        </button>
        <button class="text-white hover:text-blue-950">
          <ShoppingCartIcon  class="h-6 w-6" />
        </button>
      </div>
    </nav>

    <!-- Main -->
    <main class="px-5 pb-5">
      <!-- Gallery section -->
      <section v-if="product" class="flex flex-row gap-2 h-[280px] my-4">
        <div 
          style="box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 4px"
          :class="`flex-1 bg-gray-200 bg-cover rounded-xl h-full overflow-auto cursor-pointer hover:border hover:border-blue-400`"
        >
          <img :src="product.thumbnail" :alt="product.title" class="w-full h-full" />
        </div>
        <div class="w-[20%] flex flex-col gap-2">
          <div
            v-for="(image, key) in product.images"
            :key="key"
            style="box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 4px"
            :class="`flex-1 bg-gray-200 bg-cover rounded-xl flex items-center overflow-auto cursor-pointer hover:border hover:border-blue-400`">
            <img :key="key" :src="image" :alt="product.title" class="w-full h-full" />
          </div>
        </div>
      </section>

      <!-- Title section -->
      <section class="pb-4">
        <h1 class="font-semibold text-[22px] text-gray-700 mb-1">
          {{ product.title }}
        </h1>
        <p class="font-semibold text-[22px] text-blue-400">
        <!-- <p class="font-semibold text-[22px] text-gray-900"> -->
          {{ `$${product.priceAfterDiscount || 0}` }}
        </p>
        <div class="flex flex-row items-center">
          <p class="text-[14px] line-through text-gray-400 inline-block">
            {{ `$${product.price || 0}` }}
          </p>
          <p class="ml-1 text-[14px] text-red-500 inline-block">
            {{ `$${product.discountPercentage || 0}%` }}
          </p>
        </div>
      </section>

      <!-- Color section -->
      <section v-if="product.colors" class="pb-4">
        <h1 class="font-semibold text-[14px] text-gray-500 mb-1">
          Color
        </h1>
        <button v-for="(color, key) in product.colors" class="px-4 py-1 mr-2 rounded-md border inline-block text-gray-500 hover:bg-blue-50 hover:border-blue-400 hover:text-blue-500">
          <text class="text-[14px]">{{ color }}</text>
        </button>
      </section>

      <!-- Description section -->
      <section v-if="product.description">
        <h1 class="font-semibold text-[14px] text-gray-500 mb-1">
          Description
        </h1>
        <p class="text-[14px] text-gray-500">
          {{ product.description }}
        </p>
      </section>
    </main>
    
    <!-- Footer -->
    <Footer class="pb-3 bg-blue-500" style="margin-bottom: 60px" />

    <!-- Button floating -->
    <section class="fixed w-[100vw] bottom-0 left-0 flex justify-center ">
      <div class="w-[480px] p-2 flex flex-row h-[60px] gap-1 bg-white">
        <button class="flex-1 items-center bg-blue-950 text-gray-200 rounded-lg hover:bg-blue-900">
          <text class="font-semibold text-[15px]"> Buy </text>
        </button>
        <button class="px-3 items-center bg-white text-blue-950 border border-blue-950 rounded-lg hover:bg-blue-200">
          <ShoppingCartIcon class="h-6 w-6" />
        </button>
      </div>
    </section>
  </div>
</template>

<script setup>
import Footer from '~/components/footer/index.vue'
import { ArrowLeftIcon, ShoppingCartIcon, BellIcon } from '@heroicons/vue/24/outline'

useHead({
  title: 'Agesta Ecommerce App',
  meta: [
    { 
      name: 'description',
      content: 'Agesta ecommerce app adalah tempat jual beli online murah dan bergaransi'
    }
  ]
})
useSeoMeta({
  title: 'Agesta Ecommerce App',
  ogTitle:  'Agesta Ecommerce App',
  description: 'Agesta ecommerce app adalah tempat jual beli online murah dan bergaransi',
  ogDescription: 'Agesta ecommerce app adalah tempat jual beli online murah dan bergaransi',
  ogImage: 'https://agesta-ecommerce.netlify.app/images/youthway-logo.png'
})
const { data: product } = await useFetch(`https://dummyjson.com/products/${useRoute().params.id}`, {
  transform(product) {
    return {
      ...product,
      discountPercentage: Math.floor(product.discountPercentage),
      priceAfterDiscount: Math.floor(product.price - ((product.discountPercentage/100) * product.price)),
      colors: ['Black', 'Gray', 'Silver', 'White'],
      images: 
        product.images.length < 3 
          ? [
          'https://d33v4339jhl8k0.cloudfront.net/docs/assets/5c814e0d2c7d3a0cb9325d1f/images/5c8bc20d2c7d3a154460eb97/file-1CjQ85QAme.jpg',
          'https://image.shutterstock.com/image-vector/sample-stamp-round-grunge-sign-260nw-1449476966.jpg',
          'https://www.shutterstock.com/image-vector/sample-rubber-stamp-vector-illustration-260nw-443389582.jpg'
        ] : product.images.slice(0, 3)
    }
  }
})
</script>