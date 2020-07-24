<template>
  <div class="card-child">
    <img :src="iconImg" class="header-icon" />
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
      default: "eleme"
    }
  },
  data() {
    return {
      iconImg: "",
    };
  },
  created() {
    this.iconImg = require(`@/assets/images/${this.iconName}.png`);
  }
};
</script>

<style lang="scss" scoped>
.card-child {
  width: 60px;
  font-size: 12px;
  padding: 0px 4px;
  display: flex;
  align-items: center;
  .header-icon{
    width: 12px;
    height: 12px;
  }
  span {
    // padding-left: 2px;
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