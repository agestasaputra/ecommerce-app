<template>
  <div class="min-h-[100vh] h-full bg-white">
    <!-- Nav -->
    <nav class="flex flex-row justify-between items-center py-3 px-4 bg-blue-500">
      <NuxtLink :to="'/'">
        <img src="/images/youthway-logo.png" class="w-10" />
      </NuxtLink>
      <h1 class="font-semibold text-[16px] text-white mb-1">
        Youthway App
      </h1>
      <div class="flex flex-row">
        <button class="text-white hover:text-blue-950 mr-2">
          <BellIcon class="h-6 w-6" />
        </button>
        <button class="text-white hover:text-blue-950">
          <ShoppingCartIcon class="h-6 w-6" />
        </button>
      </div>
    </nav>

    <!-- Main -->
    <main class="pb-3">
      <!-- Search section -->
      <section class="flex flex-row pt-6 pb-3 px-5">
        <button>
          <CameraIcon class="h-6 w-6 text-gray-400 hover:text-blue-500" />
        </button>
        <input
          class="h-[35px] flex-1 mx-2 px-2 border border-gray-400 rounded-lg hover:border-blue-500"
          v-model="search.value"
          :placeholder="search.placeholder"
        />
        <button>
          <FunnelIcon class="h-6 w-6 text-gray-400 hover:text-blue-500" />
        </button>
      </section>

      <!-- Banner section -->
      <section class="py-3 px-5">
        <div class="bg-[url('/images/landing-banner-black.jpeg')] bg-cover rounded-xl h-[200px]"></div>
      </section>

      <!-- Category section -->
      <section class="py-3">
        <h1 class="px-4 font-semibold text-[16px] text-gray-900">
          Category
        </h1>
        <div class="pt-3 flex w-full overflow-auto max-h-[250px]" style="scrollbar-width: none;">
          <NuxtLink to="/" v-for="(category, key) in categories" :key="key" class="text-gray-900 hover:text-blue-500">
            <div class="p-2 bg-blue-100 rounded-lg w-[40px] mx-auto">
              <!-- <img :src="category.img" class="w-full h-full"/> -->
              <img :src="category.img" class="w-full h-full"/>
            </div>
            <p class="text-center capitalize w-[70px] text-[11px] mt-2 leading-[12px]">
              {{ category.name }}
            </p>
          </NuxtLink>
        </div>
      </section>
      
      <!-- Popular section -->
      <section class="py-3">
        <h1 class="font-semibold px-4 text-[16px] text-gray-900">
          Popular
        </h1>
        <div class="pt-3 flex w-full overflow-auto" style="scrollbar-width: none;">
          <NuxtLink
            v-for="(popular, key) in populars.products"
            :key="key"
            :to="`/products/${popular.id}`"
          >
            <div 
              class="flex flex-col rounded-lg mx-2 w-[160px] h-[250px] overflow-auto mb-1 hover:border hover:border-blue-400"
              style="box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 4px"
            >
              <div class="h-[130px]">
                <img :src="popular.thumbnail" class="w-full h-full"/>
              </div>
              <div class="flex-1 border-t p-1">
                <h1 class="text-[12px] text-gray-900 line-clamp-2">
                  {{ popular.title || '' }}
                </h1>
                <p class="text-[14px] leading-[18px] font-semibold text-gray-900 line-clamp-2">
                  {{ `$${popular.priceAfterDiscount || 0}` }}
                </p>
                <div class="leading-[18px]">
                  <p class="text-[11px] line-through text-gray-400 inline-block">
                    {{ `$${popular.price || 0}` }}
                  </p>
                  <p class="ml-1 text-[11px] text-red-500 inline-block">
                    {{ `$${popular.discountPercentage || 0}%` }}
                  </p>
                </div>
                <div class="leading-[18px]">
                  <img src="https://assets.tokopedia.net/assets-tokopedia-lite/v2/phoenix/kratos/de64305b.svg" alt="rating-icon" class="inline-block" />
                  <p class="text-[11px] text-gray-400 inline-block">
                    {{ `${popular.rating || 0}` }}
                  </p>
                </div>
              </div>
            </div>
          </NuxtLink>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <Footer class="pb-3 bg-blue-500" />
  </div>
</template>

<script setup>
import Footer from '~/components/footer/index.vue'
import { CameraIcon, BellIcon, FunnelIcon, ShoppingCartIcon } from '@heroicons/vue/24/outline'
const search = ref({
  value: '',
  placeholder: 'Search your needed'
});
const { data: categories } = await useFetch('https://dummyjson.com/products/categories', {
  transform(categories) {
    const slicedCategories = categories.slice(0, 14)
    return slicedCategories.map((item) => {
      const textToLowercase = item.toLowerCase()
      return {
        img: `/images/icon-${textToLowercase}-1.png`,
        // imageName: textToLowercase,
        name: item.split('-').join(' ')
      }
    });
  },
})
const { data: populars } = await useFetch('https://dummyjson.com/products', {
  transform(populars) {
    return {
      ...populars,
      products: populars.products.map((product) => ({
        ...product,
        discountPercentage: Math.floor(product.discountPercentage),
        priceAfterDiscount: Math.floor(product.price - ((product.discountPercentage/100) * product.price))
      }))
    }
  }
})
</script>