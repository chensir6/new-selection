<template>
  <div id="new-selection">
    <header>
      <el-row>
        <el-col :span="24">
          <div class="grid-content bg-purple-dark">
            <div class="computed">
              <div class="computed-item" style="height:12px;">
                <div
                  :class="{ active: activePath === 0 }"
                  @click="activePath = 0"
                >
                  货源搜索
                </div>
                <div
                  :class="{ active: activePath === 1 }"
                  @click="activePath = 1"
                >
                  私有选品库
                </div>
                <div
                  :class="{ active: activePath === 2 }"
                  @click="activePath = 2"
                >
                  一键上新
                </div>
                <div
                  :class="{ active: activePath === 3 }"
                  @click="activePath = 3"
                >
                  买手号管理
                </div>
              </div>
            </div>
          </div></el-col
        >
      </el-row>
    </header>
    <main v-show="activePath === 0"><sourceSearch /></main>
    <main v-show="activePath === 1"><privateSelection /></main>
    <main v-show="activePath === 2"><onclickNew /></main>
    <main v-show="activePath === 3"><buyManger /></main>
  </div>
</template>

<script>
import sourceSearch from './source-search'
import privateSelection from './private-selection'
import onclickNew from './onclick-new'
import buyManger from './buy-manger'
export default {
  components: {
    sourceSearch,
    privateSelection,
    onclickNew,
    buyManger
  },
  data() {
    return {
      activePath: 0
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../assets/css/base.less';
#new-selection {
  width: 1650px;
  padding: 24px 32px 24px 24px;
  header {
    margin-bottom: 24px;
    .el-row {
      margin-bottom: 20px;
      &:last-child {
        margin-bottom: 0;
      }
    }
    .el-col {
      border-radius: 10px;
    }
    .bg-purple-dark {
      background: #ffffff;
    }
    .bg-purple {
      background: #d3dce6;
    }
    .bg-purple-light {
      background: #e5e9f2;
    }
    .grid-content {
      border-radius: 4px;
      min-height: 64px;
      padding: 24px 32px 23px 32px;
      .computed {
        .computed-item {
          display: flex;
          .active {
            color: @activeColor;
            font-weight: bolder;
            border-bottom: 3px solid @activeColor;
          }
          div {
            height: 17px;
            font-family: MicrosoftYaHei;
            font-size: 17px;
            font-weight: normal;
            font-stretch: normal;
            line-height: 16px;
            letter-spacing: 1px;
            color: #333333;
            margin-right: 58px;
            padding-bottom: 37px;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
            &:hover {
              color: @activeColor;
            }
          }
        }
      }
    }
    .row-bg {
      padding: 10px 0;
      background-color: #f9fafc;
    }
  }
}
</style>
