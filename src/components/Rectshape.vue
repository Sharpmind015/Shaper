<template>
  <svg :width="width || length" :height="height || length">
    <rect x="0" y="0" :width="width || length" :height="height || length" :style="{strokeDasharray: perimeter, strokeDashoffset: perimeter,}" class="shape" :stroke-width="strokeWidth" :stroke="stroke"></rect>
  </svg>
</template>

<script>
export default {
  name: 'Rectshape',
  props: ['width', 'height', 'length', 'perimeter', 'strokeWidth', 'stroke']
}
</script>

