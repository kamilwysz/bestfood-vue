<script setup>
import { ref } from 'vue'
const mobileMenu = ref(false)

function toggleData() {
    this.mobileMenu = !this.mobileMenu
}
</script>
<template lang="">
    <header class="block lg:hidden ">
        <nav class="flex items-center justify-between py-5 px-10">
            <router-link to="/">
                <h1 class="text-3xl font-bold text-gray-500">
                    Best<span class="text-red-500">Food</span>
                </h1>
            </router-link>
            <button @click="toggleData()"
                class="relative">
                <font-awesome-icon icon="fa-solid fa-bars"
                    :class="mobileMenu ? 'scale-0 opacity-0' : ''"
                    class="text-gray-500 text-3xl transition duration-300 ease-in-out absolute -right-1" />
                <font-awesome-icon icon="fa-solid fa-close"
                    :class="!mobileMenu ? 'scale-0 opacity-0' : ''"
                    class="text-gray-500 text-3xl transition duration-300 ease-in-out" />
            </button>
            <div :class="mobileMenu ? '' : 'translate-x-[-100vw]'"
                class="flex flex-col gap-8 absolute bg-white top-[75px] w-full z-10 left-0 px-10 border-t py-10 h-full transition duration-300 ease-in-out">
                <router-link to="/"
                    class="font-[400] text-lg hover:text-red-700 transition duration-300 ease-in-out">Home
                </router-link>
                <router-link to="/about"
                    class="font-[400] text-lg hover:text-red-700 transition duration-300 ease-in-out">About
                </router-link>
                <router-link to="/recipes"
                    class="font-[400] text-lg hover:text-red-700 transition duration-300 ease-in-out">Recipes
                </router-link>
                <router-link to="/contact"
                    class="font-[400] text-lg hover:text-red-700 transition duration-300 ease-in-out">Contact
                </router-link>
            </div>

        </nav>
    </header>
</template>
