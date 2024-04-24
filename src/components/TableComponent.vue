<script setup>
import { ref } from 'vue'
import DataTable from './DataTable.vue';

const items = ref([
  { id: 1, name: 'Xushnud', age: 26, address: 'Toshkent', tags: ['nice', 'developer'] },
  { id: 2, name: 'Shaxboz', age: 34, address: 'Toshkent', tags: ['nice', 'developer'] },
  { id: 3, name: 'Dilshod', age: 29, address: 'Toshkent', tags: ['nice', 'developer'] },
  { id: 4, name: 'Shahzod', age: 47, address: 'Toshkent', tags: ['nice', 'developer'] },
  { id: 5, name: 'Alisher', age: 28, address: 'Toshkent', tags: ['nice', 'developer'] },
])

const columns = ref([
  { key: 'name', label: 'Name' },
  { key: 'age', label: 'Age' },
  { key: 'address', label: 'Address' },
  { key: 'tags', label: 'Tags' },
  { key: 'action', label: 'Action' },
])
</script>


<template>
  <div class="container  mt-10">
    <h1 class="text-2xl my-10">Data Table Component</h1>

    <DataTable :data="items" :columns="columns">

      <template #cell(name)="{ value }">
        <p class="text-blue-500"> {{ value }}</p>
      </template>
      <template #cell(tags)="{ value }">
        <div class="flex gap-2">
          <span class="border p-1 rounded border-green-500 bg-green-100 text-green-950" v-for="item in value">
            {{ item }}
          </span>
        </div>
      </template>
      <template #cell(action)="{ value }">
        <div class="flex gap-4">
          <button class="bg-blue-100 p-1 rounded">edit</button>
        </div>
      </template>
    </DataTable>
  </div>
</template>



