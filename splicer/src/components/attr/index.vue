<template>
  <div class="attr">
    <div class="close-all">
      <el-button type="primary" size="mini" style="width:100%">关闭所有画面</el-button>
    </div>
    <div class="control-btn">
      <el-button size="mini">置顶</el-button>
      <el-button size="mini">置底</el-button>
      <el-button size="mini">锁定</el-button>
      <el-button size="mini" @click="isPanorama=!isPanorama">
        <span v-show="isPanorama">全景</span>
        <span v-show="!isPanorama">局部</span>
      </el-button>
      <el-button size="mini">全屏</el-button>
      <el-button size="mini">扩张</el-button>
      <el-button size="mini">还原</el-button>
      <el-button size="mini">关闭</el-button>
    </div>
    <div class="title">
      <el-input placeholder="请输入画面名称" v-model="title" size="mini">
        <template slot="prepend">画面名称:</template>
      </el-input>
    </div>
    <div>
      <el-collapse v-model="activeName" accordion>
        <el-collapse-item title="画面参数" name="1">
          <div class="position-size">
            <span>水平位置:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
          <div class="position-size">
            <span>垂直位置:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
          <div class="position-size">
            <span>水平大小:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
          <div class="position-size">
            <span>垂直大小:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
        </el-collapse-item>
        <el-collapse-item title="局部显示" name="2">
          <div class="position-size">
            <span>水平位置:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
          <div class="position-size">
            <span>垂直位置:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
          <div class="position-size">
            <span>水平大小:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
          <div class="position-size">
            <span>垂直大小:</span>
            <el-input-number v-model="num" :min="1" size="mini"></el-input-number>
          </div>
        </el-collapse-item>
      </el-collapse>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeName: "1",
      isPanorama: true,
      title: "",
      num: 0
    };
  }
};
</script>

<style lang="scss" scoped>
.attr {
  padding: 0px 10px;
  .close-all {
    padding-top: 6px;
  }
  .control-btn {
    padding: 6px 0px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    .el-button {
      margin-top: 6px;
    }
  }
  .title {
    padding-top: 6px;
    padding-bottom: 6px;
    /deep/ .el-input-group__prepend {
      padding: 0px 6px;
    }
  }
  .position-size {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-bottom: 6px;
    color: #909399;
    .el-input-number {
      width: 120px;
    }
  }
}
.el-button--mini {
  padding: 6px 8px;
}
.el-button + .el-button {
  margin: 0px;
}
/deep/ .el-collapse-item__header {
  height: 40px;
  line-height: 40px;
}
/deep/ .el-collapse-item__content {
  padding-bottom: 6px;
}

</style>