<template>
  <div class="ten-pixels" title="10 ta piksel">
    <template v-if="value">
      <template v-if="['word'].includes(value.type)">
        <div
          class="text-center"
          :title="value.title"
          :style="{backgroundColor: value.backgroundColor, color: value.color}"
        >
          {{ value.text }}
        </div>
      </template>
      <template v-else-if="['photo', 'gif'].includes(value.type)">
        <img :src="valu1.photo">
      </template>
    </template>
  </div>
</template>

<script setup>
const props = defineProps({
  value: {
    default: ''
  },
});
const { value } = props;
</script>

<style lang="scss" scoped>
.ten-pixels {
  min-height: 10px;
  min-width: 10px;
  max-height: 10px;
  max-width: 10px;
  overflow: hidden;
  cursor: pointer;
  border: 0.5px solid transparent;
  font-size: 6px;
  white-space: nowrap;
  border-color: #e2e8f0;
  &:hover {
    border-color: #e2e8f0;
  }
}
</style>