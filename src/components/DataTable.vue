<script setup>
import { computed } from 'vue';

const props = defineProps({
  data: {
    type: Array,
    required: true,
  },
  columns: {
    type: Array,
    required: true,
  },
})


const displayedFieldKeys = computed(() => {
  return Object.entries(props.columns).map(([_key, value]) => value.key)
})

const format = (item, key) => {
  const field = props.columns.find((f) => f.key === key)
  return field && field.format ? field.format(item[key]) : item[key]
}
</script>

<template>
  <table class="w-full">
    <thead class="bg-gray-200">
      <tr>
        <th class="py-3 px-4 text-left" v-for="field in props.columns">
          <slot :name="`head(${field.key})`" :field="field">
            {{ field.label }}
          </slot>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr class="bg-white border-b" v-for="item in data" :key="item.id">
        <template v-for="key in displayedFieldKeys">
          <td class="px-4 py-4">
            <slot :name="`cell(${key})`" :value="format(item, (key))" :item="item">
              {{ format(item, (key)) }}
            </slot>
          </td>
        </template>
      </tr>
    </tbody>
  </table>
</template>



