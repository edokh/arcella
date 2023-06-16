<template>
  <div
    class="min-h-screen py-12 px-4 md:px-0 dark:bg-gray-900"
    :class="isReadingMode ? 'reading-mode' : 'bg-white'"
  >
    <div class="max-w-2xl mx-auto">
      <div v-if="isReadingMode == false">
        <h1 class="font-semibold text-lg dark:text-gray-300">{{ article.title }}</h1>
        <div class="tags my-4">
          <span
            v-for="tag in article.tags"
            :key="tag"
            class="px-2 py-1 mr-1 text-xs bg-[#b03337] text-white dark:bg-red-900 dark:text-gray-300"
            >{{ tag }}</span
          >
        </div>
        <img :src="article.image" alt="Article Image" class="w-full" />
      </div>
      <div class="my-6 flex flex-col sm:flex-row justify-between items-center text-gray-700">
        <div class="flex items-center">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke-width="1.5"
            stroke="currentColor"
            class="mr-1 w-5 font-semibold dark:text-gray-300"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z"
            />
          </svg>
          <span class="text-sm font-semibold dark:text-gray-300">{{ article.time }}</span>
        </div>
        <div class="flex text-xs sm:text-sm mt-4 sm:mt-0">
          <div>
            <button
              @click="share"
              type="button"
              id="shareBtn"
              class="transition duration-500 dark:hover:bg-gray-600 mr-2 inline-flex items-center rounded-xl bg-[#e4dcd1] px-3 py-1.5 font-semibold hover:bg-[#D4CCC2] dark:bg-gray-700 dark:text-gray-200"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="2.5"
                stroke="currentColor"
                class="mr-1.5 w-4"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M7.217 10.907a2.25 2.25 0 100 2.186m0-2.186c.18.324.283.696.283 1.093s-.103.77-.283 1.093m0-2.186l9.566-5.314m-9.566 7.5l9.566 5.314m0 0a2.25 2.25 0 103.935 2.186 2.25 2.25 0 00-3.935-2.186zm0-12.814a2.25 2.25 0 103.933-2.185 2.25 2.25 0 00-3.933 2.185z"
                />
              </svg>
              Share
            </button>
          </div>
          <div class="flex">
            <button
              @click="isReadingMode = !isReadingMode"
              type="button"
              class="inline-flex items-center rounded-l-xl dark:bg-gray-700 dark:text-gray-200 transition duration-500 dark:hover:bg-gray-600 bg-[#e4dcd1] pl-3 py-1.5 hover:bg-[#D4CCC2]"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="3"
                stroke="currentColor"
                class="mr-1.5 w-4 border-2 border-gray-700 text-gray-700 dark:border-gray-200 dark:text-gray-200"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25H12"
                />
              </svg>
              <span class="border-r border-gray-400 pr-2">
                {{ isReadingMode ? 'Disable reading mode' : 'Enable reading mode' }}</span
              >
            </button>

            <button
              @click="textSize > 0 ? (textSize -= 1) : (textSize = 0)"
              type="button"
              class="dark:bg-gray-700 dark:text-gray-200 transition duration-500 dark:hover:bg-gray-600 inline-flex items-center bg-[#e4dcd1] px-3 py-1.5 hover:bg-[#D4CCC2]"
            >
              A-
            </button>
            <button
              @click="textSize = 2"
              type="button"
              class="dark:bg-gray-700 dark:text-gray-200 transition duration-500 dark:hover:bg-gray-600 inline-flex items-center bg-[#e4dcd1] px-3 py-1.5 hover:bg-[#D4CCC2]"
            >
              A
            </button>
            <button
              @click="textSize < 5 ? (textSize += 1) : (textSize = 5)"
              type="button"
              class="inline-flex dark:bg-gray-700 dark:text-gray-200 transition duration-500 dark:hover:bg-gray-600 items-center bg-[#e4dcd1] px-3 py-1.5 hover:bg-[#D4CCC2] rounded-r-xl"
            >
              A+
            </button>
          </div>
        </div>
      </div>

      <h1 class="font-semibold text-lg mt-16 mb-3 dark:text-gray-300" v-if="isReadingMode">
        {{ article.title }}
      </h1>

      <div class="content dark:text-gray-300">
        <p
          class="mb-4"
          :class="textSizes[textSize]"
          v-for="paragraph in article.content.split('\n')"
          :key="paragraph"
        >
          {{ paragraph }}
        </p>
      </div>

      <div @click="toggleDark()" class="fixed right-6 bottom-6">
        <div
          class="flex border dark:bg-gray-700 dark:border-gray-200 items-center transition duration-500 ease-in-out transform hover:-translate-y-1 justify-center w-10 h-10 rounded-full bg-gray-50 cursor-pointer hover:border hover:border-solid border-gray-800"
        >
          <svg
            v-if="!isDark"
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="dark:hidden w-5 h-5 text-gray-800 dark:text-dark-contrastText"
          >
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
          </svg>
          <svg
            v-else
            width="21"
            height="21"
            viewBox="0 0 21 21"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            class="tailwind-hidden dark:block w-5 h-5 text-gray-800 dark:text-gray-200"
          >
            <path
              d="M10.5 7.2c1.81 0 3.3 1.49 3.3 3.3 0 1.81-1.49 3.3-3.3 3.3a3.31 3.31 0 0 1-3.3-3.3c0-1.81 1.49-3.3 3.3-3.3Zm0-2.2a5.5 5.5 0 1 0 0 11 5.5 5.5 0 0 0 0-11ZM2.86 11.45H.96A.96.96 0 0 1 0 10.5c0-.53.43-.95.95-.95h1.91c.53 0 .96.42.96.95s-.43.95-.96.95ZM20.05 11.45h-1.91a.96.96 0 0 1-.96-.95c0-.53.43-.95.96-.95h1.9c.53 0 .96.42.96.95s-.43.95-.95.95ZM9.55 2.86V.96c0-.53.42-.96.95-.96s.95.43.95.95v1.91c0 .53-.42.96-.95.96a.96.96 0 0 1-.95-.96ZM9.55 20.05v-1.91c0-.53.42-.96.95-.96s.95.43.95.96v1.9c0 .53-.42.96-.95.96a.96.96 0 0 1-.95-.95ZM3.42 3.42a.95.95 0 0 1 1.34 0l1.02 1c.37.37.36.98 0 1.36a.95.95 0 0 1-1.35 0L3.42 4.76a.95.95 0 0 1 0-1.34ZM15.22 15.22a.95.95 0 0 1 1.35 0l1.01 1.02a.95.95 0 1 1-1.34 1.34l-1.01-1a.95.95 0 0 1 0-1.35ZM17.58 3.42c.38.36.38.97 0 1.34l-1 1.02a.95.95 0 1 1-1.35-1.35l1-1.01a.95.95 0 0 1 1.35 0ZM5.78 15.22c.37.37.37.98 0 1.35l-1.02 1.01a.95.95 0 1 1-1.35-1.35l1.02-1a.95.95 0 0 1 1.35 0Z"
              fill="currentColor"
            ></path>
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onBeforeMount } from 'vue'
import { useDark, useToggle } from '@vueuse/core'

const isDark = useDark()
const toggleDark = useToggle(isDark)

onBeforeMount(() => {
  document.title = 'Arcella' + (' | ' + article.title || '')
})
const article = reactive({
  title: 'How to make your Vue Js application faster',
  image: '/Vue.png',
  tags: ['Vue (Learning)', 'Optimization', 'Vue.js'],
  time: '2022-06-18 23:17',
  content:
    'Have you ever wondered why your code seems slow or almost like its lagging when it runs on your user devices? Have you ever tested your Vue JS-powered application on your development machine and it runs so fast but your users seem to be complaining about the speed of your web app or having a bad user experience?\nWell if your answer is Yes or maybe a no but you want to learn how to prevent your Vue Js application from being slow, sit back and study the tips we share to help make your Vue Js application as fast and lightweight as possible.\nVue JS is a very fast and lightweight frontend framework by design, but there are certain coding decisions that you could be making that are slowing down your app. Remember that every second wasted on loading affects your user’s experience.\n\nVue.js is the newest JavaScript library, which is fast gaining popularity among web developers worldwide. Perhaps because of this novelty, it is still quite common to run into performance issues when using it for building applications. The majority of them, however, can be resolved quite easily.\nIn this guide, we will go over the key things to have in mind when creating a Vue.js-based application to achieve optimal performance.\nWhy is Vue.js gaining popularity so fast? It does have some competition in the form of Angular and React - more mature frameworks. In fact, the discussion of Vue.js vs React vs Angular seems to have no end. And in fairness, every one of the three JavaScript frameworks can be a good choice for building frontend solutions.\nAngular is considered the go-to option when we are dealing with large enterprise-scale projects. React is praised due to its extended ecosystem. Vue.js is often seen as the lightest and the most developer-friendly choice.\nHowever, there is no room for uncertain decision-making when it comes to selecting a tech stack. These common opinions may be a good indication, but the final choice is dependent on your particular scenario.\nAs Vue Storefront is based on - you guessed it - Vue.js, this is the option we advocate for. Here, we will go over why that is, which use cases it suits, and how to make the most of it, so your eCommerce store runs at its best.'
})
const share = () => {
  if (navigator.share) {
    navigator
      .share({
        text: article.title,
        url: window.location.href
      })
      .then(() => {
        console.log('Thanks for sharing!')
      })
      .catch(console.error('error!'))
  } else {
    alert(
      'The current browser does not support the share function. Please, manually share the link'
    )
  }
}

const isReadingMode = ref(false)
let textSize = ref(2)
const textSizes = ref(['text-xs', 'text-sm', 'text-base', 'text-lg', 'text-xl', 'text-2xl'])
</script>
<style>
.reading-mode {
  background-color: #ffff004f;
}
</style>
