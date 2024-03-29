<template>
  <footer>
    <!-- Subscription section -->
    <section class="bg-white pb-7">
      <div class="mx-5 flex flex-col justify-around bg-blue-500 rounded-lg p-4 mt-2 h-[150px]">
        <h1 class="w-[47%] text-[24px] leading-[28px] text-white">
          Subscribe to our newsletter?
        </h1>
        <div class="flex flex-row mt-2 h-[35px]">
          <input
            class="w-full flex-1 px-2 border border-gray-400 rounded-lg hover:border-gray-500"
            type="email"
          />
          <button class="flex items-center bg-blue-800 rounded-lg ml-1 py-1 px-2 hover:bg-blue-900">
            <text class="text-gray-200 text-[13px]">
              Subscribe
            </text>
          </button>
        </div>
      </div>
    </section>
    <!-- Menu section -->
    <section class="flex flex-row px-5 mt-4">
      <div class="flex-1">
        <h1 class="font-semibold text-[22px] text-white mb-1">
          About
        </h1>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            Blog
          </p>
        </NuxtLink>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            Our team
          </p>
        </NuxtLink>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            Contact us
          </p>
        </NuxtLink>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            Career
          </p>
        </NuxtLink>
      </div>
      <div class="flex-1">
        <h1 class="font-semibold text-[22px] text-white mb-1">
          Support
        </h1>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            Shipping
          </p>
        </NuxtLink>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            Return
          </p>
        </NuxtLink>
        <NuxtLink :to="'/'" class="text-gray-100 hover:text-blue-950">
          <p class="text-[14px] mb-1">
            FAQ
          </p>
        </NuxtLink> 
      </div>
    </section>
    <!-- Social media section -->
    <section class="px-4">
      <h1 class="font-semibold text-[22px] text-white mb-1">
        Social media
      </h1>
      <div class="flex flex-row items-center">
        <NuxtLink :to="'/'">
          <img src="/images/icon-linkedin.png" class="w-[30px] h-[30px] mr-2" />
        </NuxtLink>
        <NuxtLink :to="'/'">
          <img src="/images/icon-x.png" class="w-[30px] h-[30px] mr-2" />
        </NuxtLink>
        <NuxtLink :to="'/'">
          <img src="/images/icon-facebook.png" class="w-[30px] h-[30px] mr-2" />
        </NuxtLink>
        <NuxtLink :to="'/'">
          <img src="/images/icon-instagram.png" class="w-[30px] h-[30px]" />
        </NuxtLink>
      </div>
    </section>
  </footer>
</template>
