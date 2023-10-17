<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

const catImage = ref('')
const fetchingImage = ref(false)

const fetchCatImage = async () => {
  fetchingImage.value = true
  const response = await axios.get('https://cataas.com/cat')
  catImage.value = response.config.url + '?'  + Date.now() //из-за кеширования иногда картинка не хочет прогружаться, поэтому добавляем случайное значение к запросу

  fetchingImage.value = false
}
</script>

<template>
  <div class="row">
    <div class="col-md-12 text-center">
      <h3>Кисулькены</h3>
    </div>
    <div class="col-md-12 text-center">
      <img :src="catImage" alt="Random Cat Image" style="max-width: 400px; max-height: 400px;">
    </div>
    <div class="row mt-3">
      <div class="col-md-12 text-center">
        <button @click="fetchCatImage" class="btn btn-md btn-primary">{{ fetchingImage ? 'Зовем котика...' : 'Еще котов' }}</button>
      </div>
    </div>
  </div>
</template>
