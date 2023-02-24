<script setup lang="ts">
import { onMounted, reactive } from 'vue';

type DataType = {
  punchline: string
  setup: string
}

let data: DataType = reactive({
  punchline: '',
  setup: '',
})

const handleReload = () => window.location.reload()

onMounted(async () => {
  const res = await fetch('https://official-joke-api.appspot.com/jokes/random')
  const resData = await res.json()
  data.setup = resData.setup
  data.punchline = resData.punchline
})
</script>

<template>
  <!-- <RouterView /> -->
  <main>
    <div class="card">
      <h1>
        {{ data.setup }}
      </h1>
      <h2>
        {{ data.punchline }}
      </h2>
      <button @click="handleReload">
        Reload
      </button>
    </div>
  </main>
</template>

<style scoped>
  main {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  h1 {
    font-size: 1.375rem;
  }

  h2 {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 1rem;
  }

  button {
    background-color: maroon;
    color: blanchedalmond;
    border-radius: 0.75rem;
    padding: 0.75rem 1.25rem;
    border: none;
    cursor: pointer;
  }

  .card {
    background-color: white;
    text-align: right;
    box-shadow: 1px 1px 0.5rem grey;
    border-radius: 0.75rem;
    min-width: 37.5rem;
    margin: 0.5rem;
    padding: 1rem;
  }
</style>
