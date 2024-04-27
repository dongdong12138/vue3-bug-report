<script setup lang="ts">
import { ref } from 'vue';

const productList = ref([])
const loading = ref(false)

setTimeout(() => {
  queryProductList()
}, 1000)

// Send a Request
function queryProductList() {
  loading.value = true
  reqProductIndex().then(res => {
    console.log('res:', res)
    productList.value = res.list
  }).catch(err => {
    console.log('err:', err)
  }).finally(() => {
    console.log('productList:', productList.value)
    console.log('loading 111:', loading.value)
    loading.value = false
    console.log('loading 222:', loading.value)
  })
}

// Mock a Request
function reqProductIndex() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({})
    }, 2000)
  })
}
</script>

<template>
    <section>
      <h2>{{ loading ? 'loading...' : 'complete' }}</h2>
      <h2 v-show="!productList.length">empty</h2>
      <h2 v-show="productList.length">content</h2>
    </section>
</template>
