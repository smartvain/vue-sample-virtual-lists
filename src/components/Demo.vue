<script setup lang="ts">
import { ref } from 'vue'
import { useVirtualList, useInfiniteScroll } from '@vueuse/core'

const data = ref(Array.from(Array(50).keys(), () => 'Lorem ipsum Lorem ipsum Lorem ipsum Lorem ipsum'))

const { list, containerProps, wrapperProps } = useVirtualList(data, {
  itemHeight: 96,
  itemWidth: 300,
})

useInfiniteScroll(
  containerProps.ref,
  () => {
    data.value.push(...Array.from(Array(10).keys(), () => 'More lorem ipsum'))
  },
  { distance: 10 }
)
</script>

<template>
  <div v-bind="containerProps" class="h-screen p-2 rounded">
    <div v-bind="wrapperProps" class="max-w-sm mx-auto">
      <div
        v-for="{ index, data } in list"
        :key="index"
        class="rounded-lg h-[80px] flex flex-col px-4 justify-center bg-neutral-800 mb-4 border-neutral-600"
      >
        <h2 class="mb-2 text-2xl">Item ${{ index }}</h2>
        <p class="text-sm">{{ data }}</p>
      </div>
    </div>
  </div>
</template>