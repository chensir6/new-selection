<template>
  <div id="onclick-new">
    <el-row :gutter="16" style="margin-bottom: 15px;">
      <!-- 设置店铺 -->
      <el-col :span="4">
        <div class="grid-content">
          <div class="set-store">
            <div class="title">设置店铺</div>
            <div class="solid"></div>
            <el-form
              ref="setStoreFormRef"
              :model="setStoreForm"
              label-width="80px"
            >
              <el-form-item label="选择店铺:">
                <el-select v-model="setStoreForm.region" placeholder="全部">
                  <el-option label="区域一" value="shanghai"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="选择分类:"></el-form-item>
              <el-form-item label="一级分类:">
                <el-select v-model="setStoreForm.region" placeholder="全部">
                  <el-option label="区域一" value="shanghai"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="二级分类:">
                <el-select v-model="setStoreForm.region" placeholder="全部">
                  <el-option label="区域一" value="shanghai"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="三级分类:">
                <el-select v-model="setStoreForm.region" placeholder="全部">
                  <el-option label="区域一" value="shanghai"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label-width="0">
                <el-checkbox-group v-model="setStoreForm.type">
                  <el-checkbox label="启用高级选项" name="hight"></el-checkbox>
                </el-checkbox-group>
              </el-form-item>
              <el-form-item label-width="0">
                <el-button type="primary" size="mini" @click="onSubmitSet"
                  >设置</el-button
                >
              </el-form-item>
            </el-form>
          </div>
        </div>
      </el-col>
      <!-- 添加热搜词 -->
      <el-col :span="5">
        <div class="grid-content">
          <div class="add-search">
            <div class="title">添加热搜词</div>
            <div class="solid"></div>
            <el-form
              ref="addSearchFormRef"
              :model="addSearchForm"
              label-width="80px"
            >
              <p>标题重组热词</p>
              <el-form-item label-width="0">
                <el-input type="textarea" v-model="addSearchForm.a"></el-input>
              </el-form-item>
              <el-form-item label-width="0">
                <el-radio-group v-model="addSearchForm.resource">
                  <el-radio label="标题前加"></el-radio>
                  <el-radio label="标题后加"></el-radio>
                </el-radio-group>
              </el-form-item>
              <el-form-item label-width="0">
                <el-checkbox-group v-model="addSearchForm.type">
                  <el-checkbox
                    label="标题限制30个字"
                    name="fission"
                  ></el-checkbox>
                  <el-checkbox
                    label="裂变顺序随机打乱"
                    name="fission"
                  ></el-checkbox>
                </el-checkbox-group>
              </el-form-item>
              <el-form-item label-width="0">
                <el-button type="primary" size="mini" @click="onSubmitAdd"
                  >开始裂变</el-button
                >
              </el-form-item>
            </el-form>
          </div>
        </div>
      </el-col>
      <!-- 右边 -->
      <el-col :span="15">
        <!-- 过滤条件 -->
        <el-row style="margin-bottom: 16px;">
          <el-col :span="24">
            <div class="grid-content">
              <div class="filter-condition">
                <div class="title">过滤条件</div>
                <div class="solid"></div>
                <div class="filter-if">
                  <div class="top">
                    <div class="if-item">
                      <p>采集源：</p>
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
                      <p>商品ID：</p>
                      <el-input
                        size="mini"
                        v-model="value"
                        placeholder=""
                      ></el-input>
                    </div>
                    <div class="if-item">
                      <p>商品标题：</p>
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
                      <p>价格区间：</p>
                      <el-input v-model="input" size="mini"></el-input>-
                      <el-input v-model="input" size="mini"  style="margin-left: 10px;"></el-input>
                    </div>
                  </div>
                  <div class="if-item">
                    <el-button type="primary" size="mini">搜索</el-button>
                  </div>
                </div>
              </div>
            </div>
          </el-col>
        </el-row>
        <!-- 上货设置 -->
        <el-row>
          <el-col :span="24">
            <div class="grid-content">
              <div class="loading-set">
                <div class="title">上货设置</div>
                <div class="solid"></div>
                <div class="set">
                  <div class="set-item">
                    <p>加价比例：</p>
                    <el-input size="mini"></el-input>
                    <span>%</span>
                    <span class="scolor"
                      >*京东售价=上架SKU价格*(1+价格比例)</span
                    >
                  </div>
                  <div class="set-item">
                    <p>折扣拼团：</p>
                    <el-input size="mini"></el-input>
                    <span>%</span>
                    <span class="scolor">拼团价建议不超过89%</span>
                  </div>
                </div>
                <div class="set">
                  <div class="set-item">
                    <p>最低价处理：</p>
                    <el-radio v-model="radio" label="1">单独计算</el-radio>
                    <el-radio v-model="radio" label="2">叠加计算</el-radio>
                  </div>
                  <div class="set-item">
                    <p>最低sku加价：</p>
                    <el-input size="mini"></el-input>
                    <span>%</span>
                    <span>+</span>
                    <el-input size="mini"></el-input>
                    <span>元</span>
                  </div>
                  <div class="set-item">
                    <el-checkbox v-model="checked"
                      >设置最低价格sku为主推sku</el-checkbox
                    >
                  </div>
                </div>
                <div class="set">
                  <div class="set-item">
                    <el-checkbox v-model="checked"
                      >是否自动填充没整合的规格集</el-checkbox
                    >
                    <el-checkbox v-model="checked">过滤重复商品</el-checkbox>
                    <el-checkbox v-model="checked"
                      >上货成功后取消收藏</el-checkbox
                    >
                    <el-checkbox v-model="checked"
                      >上货成功后重新上传</el-checkbox
                    >
                  </div>
                </div>
                <div class="set">
                  <div class="set-item">
                    <p>上货接口请求频率：</p>
                    <el-input size="mini"></el-input>
                    <span>秒/次</span>
                  </div>
                  <div class="set-item">
                    <p>24小时最大购买次数：</p>
                    <el-input size="mini"></el-input>
                  </div>
                  <div class="set-item">
                    <el-button type="primary" size="mini">开始上货</el-button>
                    <el-button type="primary" size="mini" plain
                      >取消上货</el-button
                    >
                    <el-button size="mini">清除全部</el-button>
                  </div>
                </div>
              </div>
            </div>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
    <!-- 数据统计框 -->
    <el-row style="margin-bottom: 24px;">
      <div class="grid-content">
        <div class="data-box">
          <div class="title">数据统计框</div>
          <div class="solid"></div>
          <div class="statistics">
            <div class="statistics-item">
              <img src="../../assets/images/一键上新_03.png" alt="" />
              <p>商品总数：12</p>
            </div>
            <div class="statistics-item">
              <img src="../../assets/images/一键上新_05.png" alt="" />
              <p>成功总数：31</p>
            </div>
            <div class="statistics-item">
              <img src="../../assets/images/一键上新_07.png" alt="" />
              <p>失败总数：14</p>
            </div>
            <div class="statistics-item">
              <img src="../../assets/images/一键上新_09.png" alt="" />
              <p>重复总数：31</p>
            </div>
            <div class="statistics-item">
              <img src="../../assets/images/一键上新_11.png" alt="" />
              <p>过滤总数：31</p>
            </div>
          </div>
        </div>
      </div>
    </el-row>
    <!-- 发布过滤结果 -->
    <el-row style="margin-bottom: 24px;">
      <div class="grid-content">
        <div class="upload-box">
          <div class="select-item">
            <p>发布结果过滤：</p>
            <el-select v-model="value" placeholder="全部" size="mini">
              <el-option
                v-for="item in nameoptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              >
              </el-option>
            </el-select>
          </div>
          <el-button type="primary" size="mini">查询</el-button>
          <el-button type="primary" size="mini">删除</el-button>
          <div class="select-item" style="margin-left: 33px;">
            <p>上传进度</p>
            <el-progress
              :percentage="percentage"
              :strokeWidth="10"
            ></el-progress>
          </div>
        </div>
      </div>
    </el-row>
    <!-- 表格 -->
    <el-row class="onclicknew-table">
      <el-col :span="24">
        <div class="grid-content">
          <div class="table-box">
            <el-table
              ref="multipleTable"
              :data="tableData"
              tooltip-effect="dark"
              @selection-change="handleSelectionChange"
            >
              <el-table-column type="selection" width="55"> </el-table-column>
              <el-table-column label="店铺ID" width="120">
                <template slot-scope="scope">{{ scope.row.date }}</template>
              </el-table-column>
              <el-table-column prop="name" label="店铺名称" width="120">
              </el-table-column>
              <el-table-column
                prop="address"
                label="公司名称"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="登录账户"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column
                prop="address"
                label="登录状态"
                show-overflow-tooltip
              >
              </el-table-column>
              <el-table-column label="操作">
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
      setStoreFormRef: '',
      setStoreForm: {
        region: '',
        type: []
      },
      addSearchFormRef: '',
      addSearchForm: {
        a: '一行一个(最少20个热词)',
        resource: '',
        type: []
      },
      percentage: 40,
      checked: false,
      radio: '1',
      value: '',
      value1: '',
      input: '',
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
      ]
    }
  },
  methods: {
    onSubmitSet() {},
    onSubmitAdd() {},
    handleSelectionChange() {},
    importMall(index) {
      console.log(index)
    },
    format(percentage) {
      return percentage === 100 ? '满' : `${percentage}%`
    }
  }
}
</script>

<style lang="less" scoped>
@import '../../assets/css/base.less';
#onclick-new {
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
  .set-store {
    height: 501px;
    padding: 22px;
  }
  .add-search {
    height: 501px;
    padding: 22px;
    color: #666666;
    p {
      height: 40px;
      line-height: 40px;
      margin-bottom: 7px;
    }
    /deep/ .el-textarea {
      height: 80px;
    }
    /deep/ .el-textarea__inner {
      width: 269px;
      height: 60px;
      max-height: 60px;
    }
    .el-radio-group {
      display: flex;
      margin-right: 47px;
    }
  }
  .filter-condition {
    height: 234px;
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
        margin-bottom: 16px;
        align-items: center;
        .if-item {
          height: 28px;
          margin-right: 15px;
          display: flex;
          align-items: center;
        }
      }
    }
  }
  .loading-set {
    height: 252px;
    padding: 22px;
    .el-input {
      width: 120px;
    }
    span {
      padding: 0 6px;
    }
    .set {
      .el-button {
        margin: 0 16px;
      }
      display: flex;
      height: 28px;
      margin-bottom: 14px;
      .set-item {
        display: flex;
        align-items: center;
        height: 28px;
        margin-right: 20px;
      }
    }
  }
  .data-box {
    height: 146px;
    padding: 28px 38px;
    .statistics {
      display: flex;
      height: 32px;
      .statistics-item {
        margin-right: 76px;
        display: flex;
        img {
          width: 32px;
          height: 32px;
          margin-right: 9px;
        }
        p {
          line-height: 32px;
          text-align: center;
        }
      }
    }
  }
  .upload-box {
    height: 84px;
    padding: 24px 37px;
    display: flex;
    align-items: center;
    .select-item {
      padding-right: 15px;
      display: flex;
      align-items: center;
    }
    .el-button {
      margin-right: 15px;
    }
  }
  .onclicknew-table {
    .table-box {
      padding: 24px;
      /deep/ .el-table th {
        background: #f5f7fa;
      }
    }
  }
  /deep/ .el-form-item {
    color: @tabColor;
    margin-bottom: 7px;
  }
  /deep/ .el-form-item__label {
    color: @tabColor;
  }
  /deep/ .el-input__inner {
    width: 120px;
    height: 28px;
  }
  /deep/ .el-checkbox__label {
    color: @tabColor
  }
  .solid {
    border-bottom: 1px solid #cccccc;
    margin: 15px 0;
  }
  .title {
    font-size: 16px;
    font-weight: bold;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 1px;
    color: @comColor;
  }
  p {
    font-weight: normal;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 0px;
    color: @tabColor;
  }
  .scolor {
    color: @activeColor;
  }
}
</style>
