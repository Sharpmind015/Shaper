<template>
  <div>
    <div class="shape-container" v-if="shape.selected === 'Rectangle'">
      <Rectshape :width="shape.rectangleWidth" :height="shape.rectangleHeight" :perimeter="getPerimeter" :strokeWidth="strokeWidth" :stroke="shape.color"></Rectshape>
    </div>
    <div class="shape-container" v-if="shape.selected === 'Square'">
      <Rectshape :length="shape.squareLength" :perimeter="getPerimeter" :strokeWidth="strokeWidth" :stroke="shape.color"></Rectshape>
    </div>
    <div class="shape-container" v-else-if="shape.selected === 'Circle'">
      <svg :width="getCircleLine" :height="getCircleLine">
        <circle :cx="getCircleCoordinate" :cy="getCircleCoordinate" :r="shape.radius" :style="{strokeDasharray: getPerimeter, strokeDashoffset: getPerimeter,}" class="shape" :stroke-width="strokeWidth" :stroke="shape.color"></circle>
      </svg>
    </div>
  </div>
</template>

<script>
import Rectshape from './Rectshape';
export default {
  name: 'Board',
  props: ['shape'],
  data() {
    return {
      strokeWidth: 5
    }
  },
  components: {
    Rectshape
  },
  computed: {
    getPerimeter() {
      const { shape: { selected, squareLength, rectangleWidth, rectangleHeight, radius } } = this;
      if (selected === "Rectangle") {
        return 2 * (Number(rectangleWidth) + Number(rectangleHeight));
      } else if (selected === "Square") {
        return 4 * squareLength;
      } else if (selected === "Circle") {
        return 2 * Math.PI * radius;
      }
      return 0;
    },
    getCircleCoordinate() {
      return Number(this.shape.radius) + Number(this.strokeWidth);
    },
    getCircleLine() {
      return (this.shape.radius * 2) + (this.strokeWidth * 2);
    }
  }
}
</script>

<style>
.shape {
  fill: transparent;
  animation: 0.6s cubic-bezier(0.075, 0.82, 0.165, 1) 0s 1 normal forwards running shape;
}

.shape-container {
  padding: 1rem;
}

@keyframes shape {
  to {
    stroke-dashoffset: 0;
  }
}
</style>
