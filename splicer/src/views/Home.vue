<template>
  <div class="home">
    <!-- 头部菜单显示 -->
    <header>
      <el-tabs type="border-card" value="1">
        <el-tab-pane label="设备">
          <div class="card-s">
            <card title="设备">
              <card-item title="设备选择"></card-item>
              <card-item title="连接设备"></card-item>
              <card-item title="断开设备"></card-item>
              <card-item title="同步" iconName="el-icon-upload"></card-item>
              <card-item title="退出"></card-item>
            </card>
          </div>
        </el-tab-pane>
        <el-tab-pane label="主功能区">
          <div class="card-s">
            <card title="设置">
              <card-item title="创建画面" iconName="el-icon-circle-plus"></card-item>
              <card-item title="屏幕配置" iconName="el-icon-s-operation" @click.native="setting('1')"></card-item>
            </card>
            <card title="预设">
              <card-item title="用户模式" iconName="el-icon-user-solid"></card-item>
              <card-item title="保存模式" iconName="el-icon-folder-checked"></card-item>
              <card-item title="出厂设置" iconName="el-icon-s-operation"></card-item>
              <card-item title="同步" iconName="el-icon-upload"></card-item>
              <card-item
                title="打开回显"
                iconName="el-icon-s-claim"
                :isChecked="isEcho===true"
                @click.native="preinstall('5')"
              ></card-item>
              <card-item
                title="关闭回显"
                iconName="el-icon-s-release"
                :isChecked="isEcho===false"
                @click.native="preinstall('6')"
              ></card-item>
              <card-item title="回显配置" iconName="el-icon-s-order"></card-item>
            </card>
            <card title="屏幕切换">
              <card-item title="屏幕墙 1" iconName="el-icon-s-platform"></card-item>
              <card-item title="屏幕墙 2" iconName="el-icon-s-platform"></card-item>
              <div class="card-item">
                <card-child title="屏幕墙3" iconName="el-icon-s-platform"></card-child>
                <card-child title="屏幕墙4" iconName="el-icon-s-platform"></card-child>
                <card-child title="屏幕墙5" iconName="el-icon-s-platform"></card-child>
              </div>
              <div class="card-item">
                <card-child title="屏幕墙6" iconName="el-icon-s-platform"></card-child>
                <card-child title="屏幕墙7" iconName="el-icon-s-platform"></card-child>
                <card-child title="屏幕墙8" iconName="el-icon-s-platform"></card-child>
              </div>
            </card>
            <card title="对外控制">
              <div class="card-item">
                <card-child title="开屏" iconName="el-icon-s-platform"></card-child>
                <card-child title="关屏" iconName="el-icon-s-platform"></card-child>
                <card-child title="通道设置" iconName="el-icon-s-platform"></card-child>
              </div>
            </card>
            <card title="锁定">
              <card-item title="位置锁定" iconName="el-icon-lock"></card-item>
            </card>
          </div>
        </el-tab-pane>
        <el-tab-pane label="工具">
          <div class="card-s">
            <card title="高级菜单">
              <card-item title="用户"></card-item>
              <card-item title="亮度"></card-item>
              <card-item title="KFS"></card-item>
              <card-item title="多机同步"></card-item>
              <card-item title="输出关闭"></card-item>
              <card-item title="输出开启"></card-item>
              <card-item title="导入配置"></card-item>
              <card-item title="导出配置"></card-item>
              <card-item title="EDID"></card-item>
            </card>
            <card title="语言选择">
              <card-item title="语言设置"></card-item>
            </card>
            <card title="专家系统">
              <card-item title="串口设置"></card-item>
              <card-item title="网络设置"></card-item>
              <card-item title="计算器"></card-item>
              <card-item title="演示模式"></card-item>
              <card-item title="测试"></card-item>
              <card-item title="版本控制"></card-item>
              <card-item title="温度信息"></card-item>
              <card-item title="ARM升级"></card-item>
              <card-item style="width: 56px;" title="FPGA升级"></card-item>
            </card>
          </div>
        </el-tab-pane>
      </el-tabs>
    </header>
    <center>
      <!-- 侧边栏选项 -->
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
      <!-- 屏幕编辑与显示 -->
      <div class="content">
        <div class="content-title">模拟操作</div>
        <div class="content-draw">
          <!-- 窗口编辑面板 -->
          <div class="draw-panel">
            <div class="draw-content">
              <!-- 屏幕墙网格 -->
              <div class="grids">
                <!-- 屏幕分割线 -->
                <div v-for="(item,index) in 4" :key="index" class="gridlines">
                  <span>{{index+1}}</span>
                  <!-- 屏幕内部分割线 -->
                  <div v-for="(item,index) in 4" :key="index"></div>
                </div>
              </div>
              <vdr></vdr>
            </div>
          </div>
          <!-- 回显 -->
          <div class="display-list" v-show="isEcho"></div>
        </div>
      </div>
      <div class="content-compile" v-show="true">
        <div class="content-title">屏幕编辑</div>
        <div class="content-attr">
          <attr></attr>
        </div>
      </div>
    </center>
    <!-- 底部设备信息 -->
    <footer>
      <div class="status-bar">
        <div>通讯状态:</div>
        <div>
          <i v-show="true" class="el-icon-success" style="color: green;"></i>
          <i v-show="false" class="el-icon-error" style="color: red;"></i>
        </div>
        <div>设备型号:</div>
        <div title="A123411">A123411</div>
      </div>
    </footer>
    <udialog :title="dialogTitle" :dialogVisible="dialogVisible" @isDialogVisible="isDialogVisible"></udialog>
  </div>
</template>

<script>
// @ is an alias to /src
import card from "@/components/operation/Card";
import cardItem from "@/components/operation/CardItem";
import cardChild from "@/components/operation/CardChild";
import udialog from "@/components/dialog";
import vdr from "@/components/vdr";
import attr from "@/components/attr";

export default {
  name: "Home",
  data() {
    return {
      activeName: "0", // 侧边栏选项
      activeList: ["信号管理", "用户模式", "场景轮巡", "信号源分组"], // 侧边栏选项列表
      isEcho: false, // 是否回传
      dialogVisible: false, // 弹出对话框
      dialogTitle: ""
    };
  },
  methods: {
    // 预设:1-用户模式、2-保存模式、3-出厂设置、4-同步、5-打开回显、6-关闭回显、7-回显设置
    preinstall(setFn) {
      console.log(setFn);
      if (setFn === "5") {
        this.isEcho = true;
      }
      if (setFn === "6") {
        this.isEcho = false;
      }
    },
    // 设置:1-创建画面、2-屏幕配置
    setting(setFn) {
      console.log(setFn);
      if (setFn === "1") {
        this.dialogTitle = "ConfigureScreen";
        this.dialogVisible = true;
      }
      if (setFn === "2") {
        this.isEcho = false;
      }
    },
    isDialogVisible(bool) {
      this.dialogVisible = bool;
    }
  },
  components: {
    card,
    cardItem,
    cardChild,
    udialog,
    vdr,
    attr
  }
};
</script>

<style lang="scss" scoped>
.home {
  height: 100%;
  display: flex;
  flex-direction: column;
  header {
    flex: 0 0 100px;
    /deep/ .el-tabs__content {
      padding: 6px;
    }
    /deep/ .el-tabs__item {
      height: 30px;
      line-height: 30px;
    }
    /deep/ .el-tabs--border-card {
      box-shadow: none;
    }
    .card-s {
      display: flex;
      .card-item {
        height: 52px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
      }
    }
  }
  center {
    flex: 1;
    display: flex;
    .content-title {
      height: 30px;
      line-height: 30px;
      border-bottom: 1px solid #dcdfe6;
      color: #909399;
      font-size: 14px;
    }
    .content-nav {
      border-right: 1px solid #dcdfe6;
      padding-left: 10px;
      flex: 0 0 200px;
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
    .content {
      flex: 1;
      .content-draw {
        height: calc(100% - 30px);
        display: flex;
        flex-direction: column;
        // padding: 8px;
        // /* 滚动条的宽度(包括横向纵向) */
        // ::-webkit-scrollbar {
        //   width: 4px;
        //   height: 4px;
        // }
        // /* 滚动条的滑块 */
        // ::-webkit-scrollbar-thumb {
        //   background-color: #e6e8eb;
        //   border-radius: 4px;
        // }
        .draw-panel {
          flex: 1;
          min-height: 418px;
          position: relative;
          overflow: scroll;
          .draw-content {
            .grids {
              position: absolute;
              top: 1px;
              left: 1px;
              width: 768px;
              height: 432px;
              display: flex;
              flex-wrap: wrap;
              .gridlines {
                position: relative;
                display: flex;
                flex-wrap: wrap;
                box-sizing: border-box;
                width: 384px;
                height: 216px;
                border: 1px solid #dcdfe6;
                span {
                  position: absolute;
                  color: #909399;
                }
                div {
                  width: 191px;
                  height: 108px;
                  box-sizing: border-box;
                  // border: 1px dashed #dcdfe6;
                  border-right: 1px dashed #dcdfe6;
                  border-bottom: 1px dashed #dcdfe6;
                }
                div:nth-child(2n + 1) {
                  border-right: none;
                }
                div:nth-child(4) {
                  border-bottom: none;
                }
                div:nth-child(5) {
                  border-bottom: none;
                }
              }
            }
            background-color: #f5f7fa;
            border: 1px solid #dcdfe6;
            border-radius: 6px;
            // box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.12),
            //   0 0 6px 0 rgba(0, 0, 0, 0.04);
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
          }
        }
        .display-list {
          flex: 0 0 140px;
          border-top: 1px solid #dcdfe6;
        }
      }
    }
    .content-compile {
      flex: 0 0 210px;
      border-left: 1px solid #dcdfe6;
      // padding-left: 10px;
    }
  }
  footer {
    flex: 0 0 30px;
    border-top: 1px solid #dcdfe6;
    padding-left: 6px;
    background-color: #f5f7fa;
    .status-bar {
      width: 204px;
      height: 100%;
      border-right: 1px solid #dcdfe6;
      color: #909399;
      font-size: 14px;
      display: flex;
      justify-content: left;
      // align-items: center;
      div {
        line-height: 28px;
      }
      div:nth-child(2) {
        width: 20px;
        line-height: 30px;
        padding: 0px 2px;
      }
      div:nth-child(4) {
        width: 60px;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
    }
  }
}
</style>
