<script setup>
import axios from "axios";
import { ref } from 'vue'

const searchTerm = ref("")
const loading = ref(false)
const searchResults = ref("")


function searchForItem() {
      if (searchTerm.value.length && !loading.value) {
        loading.value = true
        searchResults.value = ''
        axios.get(`https://www.themealdb.com/api/json/v1/1/search.php?s=${searchTerm.value}`)
          .then(response => {
            loading.value = false
            searchResults.value = response.data.meals.slice(0, 5)
          })
          .catch(error => {
            loading.value = false
            console.log(error)
          })
      }
    }
  

</script>
<template >
    <header class="hidden lg:block">
        <nav class="flex items-center justify-between py-5 px-10">
            <router-link to="/">
                <h1 class="text-3xl font-bold text-gray-500">
                    Best<span class="text-red-600">Food</span>
                </h1>
            </router-link>
                
            <div class="flex gap-8">
                <router-link to="/"
                    class="font-[400] text-lg hover:text-red-600 transition duration-300 ease-in-out">Home
                </router-link>
                <router-link to="/about"
                    class="font-[400] text-lg hover:text-red-600 transition duration-300 ease-in-out">About
                </router-link>
                <router-link to="/recipes"
                    class="font-[400] text-lg hover:text-red-600 transition duration-300 ease-in-out">Recipes
                </router-link>
                <router-link to="/contact"
                    class="font-[400] text-lg hover:text-red-600 transition duration-300 ease-in-out">Contact
                </router-link>
            </div>

            <div class="relative">
                <label class="relative block">
                    <span class="sr-only">Search</span>
                    <span class="absolute inset-y-0 left-0 flex items-center pl-3 pr-8">
                        <font-awesome-icon icon="fa-solid fa-search"
                            class="text-gray-400" />
                    </span>
                    <input
                        class="placeholder:italic placeholder:text-slate-400 block bg-white w-full border border-slate-300 rounded-md py-2 pl-12 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
                        placeholder="Search for recipes..."
                        type="text"
                        name="search"
                        v-model="searchTerm"
                        @keyup="searchForItem()" 
                     />
                </label>
                <div class=" px-5 pt-2 pb-6 absolute top-[40px] left-0 bg-white rounded-b shadow-md w-[230px] z-[5]"
                  v-if="loading || searchResults.length">
                  <div v-if="loading"
                    class="max-w-[500px] px-5 mx-auto flex items-center justify-center">
                    <font-awesome-icon icon="fa-solid fa-circle-notch"
                      class="text-red-600 text-4xl animate-spin py-5" />
                  </div>
                  <div class="flex flex-col gap-5 divide-y-2"
                    v-if="searchResults.length && !loading">
                    <router-link
                      :to="{ name: 'recipesDetails', params: { id: `${item.strMeal.toLowerCase().split(' ').join('-')}-${item.idMeal}` } }"
                      class="pt-3 hover:text-red-700"
                      v-for="(item, index) in searchResults"
                      :key="index">
                      <p>{{ item.strMeal }}</p>
                    </router-link>

                  </div>

                </div>

            </div>
        </nav>
    </header>
</template>
