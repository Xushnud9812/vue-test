<script setup>
import ArrowIcon from './ArrowIcon.vue';

defineProps({
  data: {
    type: Array,
    required: true
  },
  indent: {
    type: Number
  }
})

const toggle = (item) => {
  item.collapsed = !item.collapsed;
};

const enter = (element) => {
  const width = getComputedStyle(element).width;

  element.style.width = width;
  element.style.position = 'absolute';
  element.style.visibility = 'hidden';
  element.style.height = 'auto';

  const height = getComputedStyle(element).height;

  element.style.width = null;
  element.style.position = null;
  element.style.visibility = null;
  element.style.height = 0;

  getComputedStyle(element).height;

  requestAnimationFrame(() => {
    element.style.height = height;
  });
}
const afterEnter = (element) => {
  element.style.height = 'auto';
}

const leave = (element) => {
  const height = getComputedStyle(element).height;

  element.style.height = height;

  getComputedStyle(element).height;

  requestAnimationFrame(() => {
    element.style.height = 0;
  });
}

</script>

<template>
  <ul class="ml-4">
    <li v-for="item in  data " :key="item.id" :style="{ 'padding-left': indent * 20 + 'px' }">
      <div @click="toggle(item)"
        class=" flex items-center gap-2  text-2xl cursor-pointer transition-colors duration-300 ">
        <ArrowIcon v-if="item.children" class="duration-300" :class="item.collapsed ? 'rotate-90' : 'rotate-0'" />
        {{ item.name }}
      </div>
      <transition name="collapse" @enter="enter" @after-enter="afterEnter" @leave="leave">
        <TreeCollapse v-if="item.children && item.collapsed" :data="item.children" :indent="indent + 1" />
      </transition>
    </li>
  </ul>
</template>



<style scoped>
.collapse-enter-active,
.collapse-leave-active {
  transition: height .2s ease-in-out;
  overflow: hidden;
}

.collapse-enter,
.collapse-leave-to {
  height: 0;
}
</style>