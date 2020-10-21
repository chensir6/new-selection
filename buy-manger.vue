<template>
  <div id="buy-manger">
    <!-- 录入 -->
    <el-row :gutter="20">
      <el-col :span="4">
        <div class="grid-content">
          <div class="buy-input">
            <div class="input-btn">
              <el-button size="mini">手动录入</el-button>
              <el-button type="primary" size="mini">自动录入</el-button>
            </div>
            <div class="buy-p">
              <p>筋斗云接码平台</p>
            </div>
            <div class="buy-item">
              <span>账号：</span>
              <el-input size="mini"></el-input>
            </div>
            <div class="buy-item">
              <span>密码：</span>
              <el-input size="mini"></el-input>
            </div>
            <div>
              <el-link href="#" target="_blank" type="primary"
                >筋斗云注册</el-link
              >
            </div>
            <div class="solid"></div>
            <div class="buy-p">
              <p>录入配置</p>
            </div>
            <div class="buy-item">
              <span>录入买手号数量：</span>
              <el-input size="mini" style="width: 80px;"></el-input>
            </div>
            <div class="buy-item">
              <span>同时录入数量：</span>
              <el-input size="mini" style="width: 80px;"></el-input>
            </div>

            <div class="solid"></div>
            <div style="margin-bottom: 19px;">
              <el-checkbox label="买手号上传到云端" name="type"></el-checkbox>
            </div>
            <div class="input-btn">
              <el-button type="primary" size="mini">开始上货</el-button>
              <el-button type="primary" size="mini" plain>取消上货</el-button>
              <el-button size="mini">清除日志</el-button>
            </div>
            <el-input type="textarea"></el-input>
            <p class="pcolor">
              备注：当前应用程序暂时支持易码平台手机号自动录入，另打码平台暂时只支持联众打码平台。
            </p>
          </div>
        </div>
      </el-col>
      <!-- 表格 -->
      <el-col :span="20">
        <div class="grid-content">
          <div class="buy-table">
            <el-table
              ref="buyTableRef"
              :data="buyTableData"
              tooltip-effect="dark"
              style="width: 100%"
              @selection-change="handleSelectionChange"
            >
              <el-table-column type="selection" width="55"> </el-table-column>
              <el-table-column label="买手号" width="120">
                <template slot-scope="scope">{{ scope.row.date }}</template>
              </el-table-column>
              <el-table-column
                prop="name"
                label="类型"
                width="120"
              ></el-table-column>
              <el-table-column prop="name" label="登陆状态"></el-table-column>
              <el-table-column
                prop="name"
                label="采集商品列表状态"
              ></el-table-column>
              <el-table-column
                prop="name"
                label="采集商品详情状态"
              ></el-table-column>
              <el-table-column
                prop="name"
                label="是否验证通过"
              ></el-table-column>
              <el-table-column
                prop="address"
                label="操作"
                show-overflow-tooltip
              >
              </el-table-column>
            </el-table>
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      buyTableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }
      ],
      multipleSelection: []
    }
  },
  methods: {
    handleSelectionChange(val) {
      this.multipleSelection = val
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../assets/css/base.less';
#buy-manger {
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .grid-content {
    background: #fff;
    border-radius: 4px;
  }
  .el-input {
    width: 130px;
  }
  .buy-input {
    height: 1154px;
    padding: 33px 23px 33px 21px;
    /deep/ .el-textarea__inner {
      max-height: 300px;
    }
    .input-btn {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      margin-bottom: 4px;
      .el-button {
        width: 100px;
        margin-bottom: 15px;
      }
    }
    .buy-p {
      border-left: 2px solid @activeColor;
      margin-bottom: 19px;
      p {
        padding-left: 6px;
      }
    }
    .buy-item {
      height: 28px;
      margin-bottom: 15px;
      padding-left: 8px;
      display: flex;
      span {
        font-weight: normal;
        font-stretch: normal;
        line-height: 23px;
        letter-spacing: 0px;
        color: #666666;
      }
    }
  }
  .buy-table {
    height: 1154px;
    padding: 24px;
    /deep/.el-table th {
      background: #f5f7fa;
    }
  }
  p {
    font-weight: normal;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 0px;
    color: #333333;
  }
  .solid {
    border-bottom: 1px solid #cccccc;
    margin: 22px 0;
  }
  .pcolor {
    color: @activeColor;
    margin-top: 15px;
    line-height: 18px;
  }
}
</style>
