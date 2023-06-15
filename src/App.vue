<template>
  <div class="article">
    <h1>{{ article.title }}</h1>
    <div class="tags">
      <span v-for="tag in article.tags" :key="tag">{{ tag }}</span>
    </div>
    <img :src="article.image" alt="Article Image" />
    <div class="actions">
      <div>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
        <span>{{ article.time }}</span>
      </div>
    </div>
    <div class="content" :class="{ 'reading-mode': isReadingMode }">
      <p>{{ article.content }}</p>
    </div>
    <div class="buttons">
      <button @click="toggleReadingMode">Enable Reading Mode</button>
      <button @click="changeTextSize('large')">Large</button>
      <button @click="changeTextSize('medium')">Medium</button>
      <button @click="changeTextSize('small')">Small</button>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const article = reactive({
  title: 'How to make your Vue Js application faster',
  image: '/vuejs.png',
  tags: ['Vue (Learning)', 'Optimization', 'Vue.js'],
  time: '2022-06-18 23:17',
  content:
    'Have you ever wondered why your code seems slow or almost like its lagging when it runs on your user devices? Have you ever tested your Vue JS-powered application on your development machine and it runs so fast but your users seem to be complaining about the speed of your web app or having a bad user experience?\nWell if your answer is Yes or maybe a no but you want to learn how to prevent your Vue Js application from being slow, sit back and study the tips we share to help make your Vue Js application as fast and lightweight as possible.\nVue JS is a very fast and lightweight frontend framework by design, but there are certain coding decisions that you could be making that are slowing down your app. Remember that every second wasted on loading affects your user’s experience.'
})

const isReadingMode = ref(false)
const textSize = ref('medium')

function toggleReadingMode() {
  isReadingMode.value = !isReadingMode.value
}

function changeTextSize(size) {
  textSize.value = size
}

// const contentClasses = {
//   'text-large': textSize.value === 'large',
//   'text-medium': textSize.value === 'medium',
//   'text-small': textSize.value === 'small'
// }
</script>

<style scoped>
.w-6 {
  width: 1.5rem;
}
.article {
  max-width: 500px;
  margin: 0 auto;
}
.article h1 {
  font-size: medium;
  font-weight: 500;
}
.article img {
  width: 100%;
}
.tags {
  margin: 12px 0;
}
.tags span {
  margin-right: 5px;
  color: #fff;
  background-color: #b03337;
  padding: 3px 5px;
  font-size: x-small;
}

.content {
  margin-top: 20px;
  line-height: 1.6;
}

.reading-mode .content {
  background-color: #f5f5f5;
  padding: 10px;
}

.text-large {
  font-size: 18px;
}

.text-medium {
  font-size: 16px;
}

.text-small {
  font-size: 14px;
}
</style>
