<template>
  <div class="content-nav">
    <div class="content-title">{{activeList[parseInt(activeName)]}}</div>
    <el-collapse v-model="activeName" accordion>
      <el-collapse-item name="0">
        <template slot="title">
          <i class="header-icon el-icon-s-tools"></i>
          <span class="content-list-title">信号管理</span>
        </template>
        <div class="content-list">信号管理</div>
      </el-collapse-item>
      <el-collapse-item name="1">
        <template slot="title">
          <i class="header-icon el-icon-user-solid"></i>
          <span class="content-list-title">用户模式</span>
        </template>
        <div class="content-list">用户模式</div>
      </el-collapse-item>
      <el-collapse-item name="2">
        <template slot="title">
          <i class="header-icon el-icon-video-camera-solid"></i>
          <span class="content-list-title">场景轮巡</span>
        </template>
        <div class="content-list">场景轮巡</div>
      </el-collapse-item>
      <el-collapse-item name="3">
        <template slot="title">
          <i class="header-icon el-icon-s-grid"></i>
          <span class="content-list-title">信号源分组</span>
        </template>
        <div class="content-list">信号源分组</div>
      </el-collapse-item>
    </el-collapse>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeName: "0", // 侧边栏选项
      activeList: ["信号管理", "用户模式", "场景轮巡", "信号源分组"] // 侧边栏选项列表
    };
  }
};
</script>

<style lang="scss" scoped>
.content-nav {
  border-right: 1px solid #dcdfe6;
  padding-left: 10px;
  flex: 0 0 200px;
  .content-title {
    height: 30px;
    line-height: 30px;
    border-bottom: 1px solid #dcdfe6;
    color: #909399;
    font-size: 14px;
  }
  .header-icon {
    padding-right: 6px;
    // padding-bottom: 1px;
    // padding-top: 2px;
    font-size: 16px;
  }
  .el-collapse {
    border-top: none;
  }
  .content-list {
    border-top: 1px solid #ebeef5;
  }
  .content-list-title:hover {
    color: #409eff;
  }
  /deep/ .el-collapse-item__header {
    height: 40px;
    line-height: 40px;
  }
}
</style>