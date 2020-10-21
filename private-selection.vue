<template>
  <div id="private-selection">
    <el-row :gutter="25">
      <el-col :span="8">
        <div class="grid-content">
          <div class="base-oper">
            <div class="title">
              商品操作
            </div>
            <div class="solid"></div>
            <div class="mall-btn">
              <div class="btn-item">
                <el-button type="primary" size="mini">批量添加尺寸</el-button>
              </div>
              <div class="btn-item">
                <el-button type="primary" size="mini">标记优选商品</el-button>
              </div>
              <div class="btn-item">
                <el-button type="primary" size="mini" plain
                  >取消标记优选商品</el-button
                >
              </div>
              <div class="btn-item">
                <el-button type="primary" size="mini">一键上新</el-button>
              </div>
              <div class="btn-item">
                <el-button type="primary" size="mini" plain>取消收藏</el-button>
              </div>
            </div>
          </div>
        </div>
      </el-col>
      <el-col :span="16">
        <div class="grid-content">
          <div class="filter-box">
            <div class="title">列表筛选</div>
            <div class="solid"></div>
            <div class="filter-if">
              <div class="top">
                <div class="if-item">
                  <p>采购来源：</p>
                  <el-select v-model="value" placeholder="全部" size="mini">
                    <el-option
                      v-for="item in nameoptions"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    ></el-option>
                  </el-select>
                </div>
                <div class="if-item">
                  <p>筛选时间：</p>
                  <el-select v-model="value" placeholder="全部" size="mini">
                    <el-option
                      v-for="item in nameoptions"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    ></el-option>
                  </el-select>
                  <el-date-picker
                    v-model="value1"
                    type="daterange"
                    range-separator="-"
                    start-placeholder="开始日期"
                    end-placeholder="结束日期"
                    size="mini"
                    style="width: 318px;"
                  >
                  </el-date-picker>
                </div>
                <div class="if-item">
                  <p>优选商品：</p>
                  <el-select v-model="value" placeholder="全部" size="mini">
                    <el-option
                      v-for="item in nameoptions"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    ></el-option>
                  </el-select>
                </div>
              </div>
              <div class="bottom">
                <div class="if-item">
                  <p>编辑状态：</p>
                  <el-select v-model="value" placeholder="全部" size="mini">
                    <el-option
                      v-for="item in nameoptions"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    ></el-option>
                  </el-select>
                </div>
                <div class="if-item">
                  <p>价格区间：</p>
                  <el-input v-model="input" size="mini"></el-input>-
                  <el-input v-model="input" size="mini" style="margin-left: 10px;"></el-input>
                </div>
                <div class="if-item">
                  <p>商品ID：</p>
                  <el-input
                    size="mini"
                    v-model="input"
                    placeholder=""
                  ></el-input>
                </div>
                <div class="if-item">
                  <el-button type="primary" size="mini">搜索</el-button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row class="private-table">
      <el-col :span="24">
        <div class="grid-content">
          <div class="table-box">
            <div class="tip">
              尊敬的用户：您好，为提高私有选品库模块的性能，系统将只保留近3个月的非精选商品数据，为保证部分精选商品不被清理，请将需要保留的商品标记为精选商品
            </div>
            <el-table
              ref="multipleTable"
              :data="tableData"
              tooltip-effect="dark"
              style="width: 100%"
              @selection-change="handleSelectionChange"
            >
              <el-table-column type="selection" width="55"></el-table-column>
              <el-table-column label="序号" type="index" width="50">
              </el-table-column>
              <el-table-column label="采购来源" width="120">
                <template slot-scope="scope">{{ scope.row.date }}</template>
              </el-table-column>
              <el-table-column prop="name" label="优选商品" width="120">
              </el-table-column>
              <el-table-column
                prop="address"
                label="商品信息"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="价格（元）"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="库存"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="销量"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="更新时间"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="收藏时间"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="有效日期"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column label="操作结果">
                <template slot-scope="scope">
                  <el-button
                    size="mini"
                    type="primary"
                    plain
                    @click="importMall(scope.$index)"
                    >导入店铺</el-button
                  >
                </template>
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
      value1: '',
      value: '',
      nameoptions: [
        {
          value: '0',
          label: '全部'
        }
      ],
      tableData: [
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-08',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-06',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-07',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }
      ],
      multipleSelection: [],
      input: ''
    }
  },
  methods: {
    handleClick() {},
    handleSelectionChange() {}
  }
}
</script>

<style lang="less" scoped>
@import '../../assets/css/base.less';
#private-selection {
  .base-oper {
    height: 188px;
    padding: 22px;
    .title {
      font-size: 16px;
      font-weight: bold;
      font-stretch: normal;
      line-height: 23px;
      letter-spacing: 1px;
      color: #333333;
    }
    .mall-btn {
      display: flex;
      flex-wrap: wrap;
      .btn-item {
        display: flex;
        margin-right: 30px;
        margin-bottom: 10px;
      }
    }
  }
  .filter-box {
    height: 188px;
    padding: 22px;
    .filter-if {
      .el-select {
        width: 130px;
        margin-right: 10px;
      }
      .el-input {
        width: 120px;
        margin-right: 10px;
      }
      .top {
        display: flex;
        margin-bottom: 16px;
        align-items: center;
        .if-item {
          height: 28px;
          margin-right: 15px;
          display: flex;
          align-items: center;
        }
      }
      .bottom {
        display: flex;
        .if-item {
          height: 28px;
          margin-right: 15px;
          display: flex;
          align-items: center;
          &:last-child {
            margin-left: 60px;
          }
        }
      }
    }
  }
  .private-table {
    .table-box {
      height: 1007px;
      .tip {
        color: #f97c28;
        margin: 14px 0px;
      }
      padding: 15px 20px;
      /deep/ .el-table th {
        background: #f5f7fa;
      }
    }
  }
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .grid-content {
    border-radius: 10px;
    background: #fff;
  }
  .solid {
    border-bottom: 1px solid #e5e5e5;
    margin: 15px 0px;
  }
  .title {
    font-size: 16px;
    font-weight: bold;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 1px;
    color: #333333;
  }
  p {
    font-weight: normal;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 0px;
    color: #666666;
  }
}
</style>
