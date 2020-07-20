<template>
  <div
    :style="`height: ${vdrHeigth}px; width: ${vdrWidth}px; border: 1px solid #dcdfe6; border-radius: 6px; position: relative;`"
  >
    <vdr
      :min-width="66"
      :min-height="66"
      v-on:dragging="onDrag"
      v-on:resizing="onResize"
      :parent="true"
      :snap="true"
      :snap-tolerance="10"
      :z-index="1"
      :w="100"
      :h="100"
      :x="100"
      :y="100"
    >
      <vdr-window>
        <p>Title:Hello</p>
        <p>X: {{ x }}</p>
        <p>Y: {{ y }}</p>
        <p>Width: {{ width }}</p>
        <p>Height: {{ height }}</p>
      </vdr-window>
    </vdr>
    <!-- :snap="true" 开启吸附功能
    :snapTolerance="10" 距离小于10px开始吸附-->
    <vdr
      :parent="true"
      :debug="false"
      :min-width="66"
      :min-height="66"
      :isConflictCheck="true"
      :snap="true"
      :snapTolerance="10"
      :z-index="2"
      :w="200"
      :h="200"
      :x="100"
      :y="100"
    >
      <vdr-window>
        <p>Title:Hello</p>
        <p>X: {{ x }}</p>
        <p>Y: {{ y }}</p>
        <p>Width: {{ width }}</p>
        <p>Height: {{ height }}</p>
      </vdr-window>
    </vdr>
  </div>
</template>

<script>
import vdr from "vue-draggable-resizable-gorkys";
import "vue-draggable-resizable-gorkys/dist/VueDraggableResizable.css";
import vdrWindow from "@/components/vdr/VdrWindow/";
export default {
  data: function() {
    return {
      vdrHeigth: 432, // 编辑幕布宽度
      vdrWidth: 768, // 编辑幕布高度
      width: 0,
      height: 0,
      x: 0,
      y: 0
    };
  },
  methods: {
    onResize: function(x, y, width, height) {
      this.x = x;
      this.y = y;
      this.width = width;
      this.height = height;
    },
    onDrag: function(x, y) {
      this.x = x;
      this.y = y;
    }
  },
  components: {
    vdr,
    vdrWindow
  }
};
</script>

<style lang="scss" scoped>
.vdr {
  border-radius: 8px;
  border: 1px solid #000000;
  background: #409eff;
}
</style>