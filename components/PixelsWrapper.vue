<template>
  <div class="pixels-wrapper" :style="{width: (length * 10) + 'px'}">
    <slot></slot>
  </div>
</template>

<script setup>
const props = defineProps({
  length: {
    type: Number,
    required: false,
    default: 100
  },
});
const { length } = props;

</script>

<style lang="scss" scoped>
.pixels-wrapper {
  display: flex;
  flex-wrap: wrap;
  width: 1000px;
  margin: 0 auto;
}
</style>