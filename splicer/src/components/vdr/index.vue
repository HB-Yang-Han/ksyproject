<template>
  <div class="draw-vdr">
    <!-- 网格 -->
    <div class="grids" :style="`height: ${vdrHeigth}px; width: ${vdrWidth}px;`">

    </div>
    <div
      @wheel="mouseWheel"
      :style="`height: ${vdrHeigth}px; width: ${vdrWidth}px; border: 1px solid #dcdfe6; position: relative;`"
    >
      <vdr
        :min-width="40"
        :min-height="40"
        v-on:dragging="onDrag"
        v-on:resizing="onResize"
        :draggable="true"
        :parent="true"
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
      :snapTolerance="10" 距离小于10px开始吸附
      :draggable="true" 控制组件是否可以拖动-->
      <vdr
        :parent="true"
        :debug="false"
        :min-width="40"
        :min-height="40"
        :isConflictCheck="true"
        :draggable="true"
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
  mounted() {},
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
    },
    mouseWheel(e) {
      console.log(e.wheelDelta);
      let ratio = 1080 / 1920;
      if (e.wheelDelta > 0) {
        this.vdrHeigth = Math.floor(this.vdrHeigth + this.vdrHeigth * 0.05);
        this.vdrWidth = Math.floor(this.vdrHeigth / ratio);
        // 将画布最大限制成最大物理分辨率;
        if (this.vdrWidth > 1920) {
          this.vdrHeigth = 1080;
          this.vdrWidth = 1920;
        }
      } else {
        this.vdrHeigth = Math.floor(this.vdrHeigth - this.vdrHeigth * 0.05);
        this.vdrWidth = Math.floor(this.vdrHeigth / ratio);
        if (this.vdrWidth < 702) {
          this.vdrHeigth = 396;
          this.vdrWidth = 702;
        }
      }

      if (this.vdrWidth > 960) {
        this.$emit("alignCenter", false);
      } else {
        this.$emit("alignCenter", true);
      }
      this.$nextTick(() => {
        // 当父窗口大小发生变化时子窗口必须重载不然无法确定拖动范围
        window.dispatchEvent(new Event("resize"));
      });
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
  // border-radius: 8px;
  border: 1px solid #000000;
  background: #409eff;
}
.draw-vdr{
  position: relative;
  .grids{
    position: absolute;
    top: 0px;
    left: 0px;
  }
}
</style>