<template>
  <div>
    <div class="set-screen">
      <div>
        <span>屏幕分辨率:</span>
        <el-select v-model="resolutionValue" placeholder="请选择分辨率" size="mini" style="width:160px">
          <el-option
            v-for="item in resolution"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          ></el-option>
        </el-select>
      </div>
      <div>
        <span>屏幕刷新HZ:</span>
        <el-select v-model="hertzValue" placeholder="请选择HZ" size="mini" style="width: 100px;">
          <el-option
            v-for="item in hertz"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          ></el-option>
        </el-select>
      </div>
      <div style="padding-top: 4px;">
        <el-checkbox v-model="lcdMode">
          <i style="font-size: 12px;">LCD模式</i>
        </el-checkbox>
      </div>
    </div>
    <div class="set-screen">
      <div>
        <span>行数:</span>
        <el-input-number
          v-model="rowNum"
          :min="1"
          :max="10"
          size="mini"
          style="width: 100px;"
        ></el-input-number>
      </div>
      <div>
        <span>列数:</span>
        <el-input-number
          v-model="columnNum"
          :min="1"
          :max="10"
          size="mini"
          style="width: 100px;"
        ></el-input-number>
      </div>
      <div>
        <el-button type="danger" size="mini">删除屏幕墙</el-button>
      </div>
      <div>
        <el-button type="primary" size="mini">添加屏幕墙</el-button>
      </div>
    </div>
  </div>
</template>

<script>
// 分辨率选项
const resolution = [
  {
    value: "1024*768",
    label: "1024*768"
  },
  {
    value: "1280*720",
    label: "1280*720"
  },
  {
    value: "1280*768",
    label: "1280*768"
  },
  {
    value: "1280*800",
    label: "1280*800"
  },
  {
    value: "1280*960",
    label: "1280*960"
  },
  {
    value: "1280*1024",
    label: "1280*1024"
  }
];
let resolutionValue = "1280*960";

// 赫兹选项
const hertz = [
  {
    value: "60HZ",
    label: "60HZ"
  },
  {
    value: "50HZ",
    label: "50HZ"
  }
];
let hertzValue = "50HZ";
export default {
  props: {
    data: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      resolution,
      resolutionValue,
      hertz,
      hertzValue,
      rowNum: 0,
      columnNum: 0,
      lcdMode: false
    };
  }
};
</script>

<style lang="scss" scoped>
.set-screen {
  font-size: 12px;
  display: flex;
  flex-wrap: nowrap;
  justify-content: space-between;
  margin-bottom: 8px;
  span {
    padding-right: 6px;
  }
}
</style>