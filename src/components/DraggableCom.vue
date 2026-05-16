<template>
  <div
    class="draggable"
    @mousedown="startDrag"
    @mouseup="endDrag"
    @mousemove="doDrag"
    :style="styleObject"
  >
    <!-- 拖拽的内容 -->
    <slot>拽我</slot>
  </div>
</template>
 
<script>
export default {
  name: "DraggableCom",
  data() {
    return {
      dragging: false,
      mouseX: 0,
      mouseY: 0,
      initialX: 0,
      initialY: 0,
      offsetX: 0,
      offsetY: 0
    };
  },
  computed: {
    styleObject() {
      return {
        position: 'absolute',
        left: `${this.initialX + this.offsetX}px`,
        top: `${this.initialY + this.offsetY}px`
      };
    }
  },
  methods: {
    startDrag(event) {
      this.dragging = true;
      this.initialX = event.clientX - this.offsetX;
      this.initialY = event.clientY - this.offsetY;
    },
    endDrag() {
      this.dragging = false;
    },
    doDrag(event) {
      if (this.dragging) {
        this.offsetX = event.clientX - this.initialX;
        this.offsetY = event.clientY - this.initialY;
      }
    }
  }
};
</script>
 
<style>
.draggable {
  cursor: move;
  /* 其他样式 */
}
</style>
