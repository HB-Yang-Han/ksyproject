<template>
  <el-dialog
    title="屏幕参数设置"
    :visible.sync="isVisible"
    width="900px"
    top="8vh"
    @close="isSubmit(false)"
    center
  >
    <div class="setting">
      <div class="setting-port">
        <ul>
          <li v-for="(val,index) in portList" :key="index" @click="portPut(val)">Port{{val}}</li>
        </ul>
        <div class="mapping">
          <el-button type="primary" size="mini">自动映射</el-button>
        </div>
      </div>
      <div class="setting-parameter">
        <el-tabs type="border-card">
          <!-- 屏幕墙 -->
          <el-tab-pane label="屏幕墙-1">
            <!-- 屏幕墙编辑面板 -->
            <cs-parameter :data="data"></cs-parameter>
            <!-- 屏幕列表辑面板 -->
            <div class="drawing">
              <div class="resolution-x" :style="`width: ${column*192}px;`">
                <div v-for="(item,index) in column" :key="index">
                  <el-input
                    v-model="ranksRow[index]"
                    placeholder="请输入内容"
                    size="mini"
                    @input="ranks('column',index,ranksRow[index])"
                  ></el-input>
                </div>
              </div>
              <div class="resolution-y" :style="`height: ${row*108}px;`">
                <div v-for="(item,index) in row" :key="index">
                  <el-input
                    v-model="ranksColumn[index]"
                    placeholder="请输入内容"
                    size="mini"
                    @input="ranks('row',index,ranksColumn[index])"
                  ></el-input>
                </div>
              </div>
              <div class="drawing-list" :style="`width: ${column*192}px; height: ${row*108}px;`">
                <div
                  v-for="(item,index) in displayList"
                  :key="index"
                  class="drawing-item"
                  @click="displaySelect(index)"
                  :class="{'display-select':displayIndex === index}"
                >
                  <div v-show="displayIndex !== index">
                    <p>屏幕编号:{{item.title}}</p>
                    <p>水平大小:{{item.resolutionX}}</p>
                    <p>垂直大小:{{item.resolutionY}}</p>
                    <p>输出映射:{{item.settingPort}}</p>
                  </div>
                  <div div v-show="displayIndex === index">
                    <p>屏幕编号:{{item.title}}</p>
                    <p>水平大小:{{item.resolutionX}}</p>
                    <p>垂直大小:{{item.resolutionY}}</p>
                    <!-- <p>
                      水平大小:
                      <el-input
                        v-model="item.resolutionX"
                        placeholder="请输入内容"
                        size="mini"
                        style="width:100px"
                      ></el-input>
                    </p>
                    <p>
                      垂直大小:
                      <el-input
                        v-model="item.resolutionY"
                        placeholder="请输入内容"
                        size="mini"
                        style="width:100px"
                      ></el-input>
                    </p>-->
                    <p>输出映射:Port{{item.settingPort}}(点击Port修改)</p>
                  </div>
                </div>
              </div>
            </div>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
    <span slot="footer" class="dialog-footer">
      <el-button @click="isSubmit(false)" size="mini">取 消</el-button>
      <el-button type="primary" @click="isSubmit(true)" size="mini">确 定</el-button>
    </span>
  </el-dialog>
</template>

<script>
import csParameter from "@/components/dialog/ConfigureScreenParameter";

// 显示屏数据列表
let displayList = [
  {
    title: "display1",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display2",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display3",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display4",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display5",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display6",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display7",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  },
  {
    title: "display8",
    resolutionX: 1920,
    resolutionY: 1080,
    settingPort: 1
  }
];

export default {
  props: {
    dialogVisible: {
      type: Boolean,
      default: false
    },
    data: {
      type: Object,
      default: () => {}
    }
  },
  data() {
    return {
      isVisible: this.dialogVisible, // 窗口是否显示
      portList: [], // 端口port列表
      displayLists: [], // 屏幕墙列表
      row: 2,
      column: 4, // 屏幕列表行
      resolution: "1920*1080",
      displayList, // 屏幕数据列表
      displayIndex: undefined, // 当前选中屏幕
      ranksRow: [], // 行顶部分辨率列表
      ranksColumn: [] // 列左部分辨率列表
    };
  },
  created() {
    this.portList = Array.from({ length: 90 }, (v, k) => 90 - k);
    this.ranksRow = Array.from({ length: this.column }, () => 1920);
    this.ranksColumn = Array.from({ length: this.row }, () => 1080);
  },
  methods: {
    isSubmit(bool) {
      if (bool) {
        console.log("确定");
      } else {
        console.log("取消");
      }
      this.$emit("isDialogVisible", false); // 退出关闭弹窗
    },
    portPut(io) {
      // 当前点击的port端口
      // console.log(io);
      if (this.displayIndex != undefined) {
        displayList[this.displayIndex].settingPort = io;
      } else {
        console.log("请选择屏幕！");
      }
    },
    displaySelect(index) {
      // 当前选中的屏幕
      // console.log(index);
      this.displayIndex = index;
    },
    ranks(rc, count, val) {
      //修改行与列的分辨率
      console.log(rc, count);
      if (rc === "column") {
        // 列分辨率设置
        this.displayList.forEach((ele, index) => {
          // console.log(index,ele);
          if (index % this.column === 0) {
            displayList[index + count].resolutionX = val;
            // console.log(index, ele);
          }
        });
      }
      if (rc === "row") {
        // 行分辨率设置
        let start = count * this.column;
        for (let i = start; i < start + this.column; i++) {
          displayList[i].resolutionY = val;
        }
      }
    }
  },
  components: {
    csParameter
  }
};
</script>

<style lang="scss" scoped>
.setting {
  display: flex;
  .setting-port {
    background: #fff;
    border: 1px solid #dcdfe6;
    box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.12), 0 0 6px 0 rgba(0, 0, 0, 0.04);
    padding: 6px;
    ul {
      width: 300px;
      display: flex;
      flex-wrap: wrap;
      flex-direction: row-reverse;
      border-left: 1px solid #dcdfe6;
      border-top: 1px solid #dcdfe6;
      li {
        width: 50px;
        height: 28px;
        box-sizing: border-box;
        border-right: 1px solid #dcdfe6;
        border-bottom: 1px solid #dcdfe6;
        text-align: center;
        line-height: 28px;
        font-size: 12px;
      }
      li:hover {
        background-color: #f5f7fa;
        color: #409eff;
        cursor: pointer;
      }
    }
    .mapping {
      display: flex;
      justify-content: center;
      padding-top: 6px;
    }
  }
  .setting-parameter {
    width: 556px;
    margin-left: 4px;
    position: relative;
    // 屏幕列表辑面板
    .drawing {
      border: 1px solid #dcdfe6;
      width: 482px;
      height: 328px;
      padding-top: 20px;
      padding-left: 40px;
      position: relative;
      font-size: 12px;
      color: #909399;
      .resolution-x {
        display: flex;
        position: absolute;
        height: 20px;
        top: 0px;
        background: #e4e7ed;
        div {
          // border: 1px solid #dcdfe6;
          box-sizing: border-box;
          width: 192px;
          height: 20px;
          /deep/ .el-input--mini .el-input__inner {
            height: 100%;
            line-height: 20px;
            border-radius: 0px;
            text-align: center;
            background: #e4e7ed;
          }
        }
      }
      .resolution-y {
        display: flex;
        flex-direction: column;
        position: absolute;
        width: 40px;
        left: 0px;
        background: #e4e7ed;
        div {
          // border: 1px solid #dcdfe6;
          box-sizing: border-box;
          width: 40px;
          height: 108px;
          /deep/ .el-input--mini .el-input__inner {
            height: 100%;
            line-height: 20px;
            border-radius: 0px;
            text-align: center;
            padding: 0px;
            background: #e4e7ed;
          }
        }
      }
      // display: flex;
      // justify-content: flex-start;
      // align-items: center;
      overflow: scroll;
      .drawing-list {
        // margin: auto;
        background: #f5f7fa;
        display: flex;
        flex-wrap: wrap;
        .drawing-item {
          box-sizing: border-box;
          border: 1px solid #dcdfe6;
          width: 192px;
          height: 108px;
          p {
            font-size: 12px;
            color: #909399;
            padding: 2px;
            text-align: left;
          }
          /deep/ .el-input--mini .el-input__inner {
            height: 20px;
            line-height: 20px;
          }
          text-align: center;
        }
        .display-select {
          background: #e4e7ed;
        }
      }
    }
    .add-tab-pane {
      position: absolute;
      z-index: 100;
      top: 1px;
      right: 0px;
    }
    /deep/ .el-tabs__content {
      height: 422px;
      padding: 8px;
    }
    /deep/ .el-tabs__item {
      height: 30px;
      line-height: 30px;
      padding: 0px 6px !important;
      font-size: 12px;
    }
    /deep/ .el-tabs__nav-prev {
      line-height: 30px;
    }
  }
}
</style>