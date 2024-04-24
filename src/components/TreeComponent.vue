<script setup>
import { ref } from 'vue'
import TreeCollapse from './TreeCollapse.vue';

const treeData = ref([
  {
    id: 1, name: 'item 1', collapsed: false,
    children: [
      {
        id: 2, name: 'item 1.1', collapsed: false,
        children: [
          { id: 3, name: 'item 1.1.1', collapsed: false, },
          { id: 4, name: 'item 1.1.2', collapsed: false },
          { id: 5, name: 'item 1.1.3', collapsed: false },
        ]
      },
      { id: 6, name: 'item 1.2', collapsed: false }
    ]
  },
  { id: 7, name: 'item 2', collapsed: false }
]);

</script>

<template>
  <div class="container border-b pb-10">
    <h1 class="text-2xl my-10 ">Tree Collapse Component</h1>
    <TreeCollapse :data="treeData" :indent="0" />
  </div>
</template>



