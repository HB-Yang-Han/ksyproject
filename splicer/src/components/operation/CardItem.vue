<template>
  <div class="card-item" :class="{'card-item-bg':isChecked}">
    <div>
      <i class="header-icon" :class="iconName"></i>
    </div>
    <div>
      <span>{{title}}</span>
    </div>
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
    },
    isChecked: {
      type: Boolean,
      default: false
    }
  }
};
</script>

<style lang="scss" scoped>
.card-item {
  font-size: 12px;
  width: 52px;
  height: 52px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 4px;
  margin: 0px 1px;
  border-radius: 6px;
  .header-icon {
    font-size: 34px;
  }
  div {
    text-align: center;
  }
  span {
    color: #909399;
  }
}
.card-item-bg {
  background-color: #f5f7fa;
  span {
    color: #409eff;
  }
}
.card-item:hover {
  cursor: pointer;
  background-color: #f5f7fa;
  span {
    color: #409eff;
  }
}
</style>