<template>
  <div class="card-child">
    <i :class="iconName"></i>
    <span>{{title}}</span>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "未定义"
    },
    iconName: {
      type: String,
      default: "el-icon-eleme"
    }
  }
};
</script>

<style lang="scss" scoped>
.card-child {
  width: 60px;
  font-size: 12px;
  padding: 0px 4px;
  span {
    color: #909399;
  }
  span:hover {
    color: #409eff;
  }
}
.card-child:hover {
  cursor: pointer;
  background-color: #f5f7fa;
}
</style>