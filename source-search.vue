<template>
  <div id="source-search">
    <el-row>
      <el-col :span="24">
        <div class="grid-content bg-purple-dark">
          <div class="search-select">
            <div class="search-tabs">
              <el-tabs
                v-model="activeName"
                type="card"
                @tab-click="handleClick"
              >
                <el-tab-pane label="关键词采集" name="first">
                  <div class="key-collection">
                    <div class="malls">
                      <div
                        class="malls-item"
                        v-for="(item, index) in malls"
                        :key="index"
                        :class="{ active: activeMall === item }"
                        @click="onMalls(item)"
                      >
                        {{ item }}
                      </div>
                    </div>
                    <div class="mall-main">
                      <div class="web-collection">
                        <div class="collection-item">
                          <el-radio v-model="radio" label="1"
                            >云端采集<span class="pcolor"
                              >(无需账号)</span
                            ></el-radio
                          >
                          <el-radio v-model="radio" label="2"
                            >本地采集<span class="pcolor"
                              >(需登陆账号)</span
                            ></el-radio
                          >
                        </div>
                        <div class="collection-item">
                          <div class="if-item">
                            <p>拼多多账号：</p>
                            <el-select
                              v-model="value"
                              placeholder="178****4033"
                              size="mini"
                            >
                              <el-option
                                v-for="item in nameoptions"
                                :key="item.value"
                                :label="item.label"
                                :value="item.value"
                              ></el-option>
                            </el-select>
                          </div>
                          <div class="if-item">
                            <el-button type="primary" size="mini"
                              >网页采集</el-button
                            >
                          </div>
                        </div>
                        <div class="collection-item">
                          <div class="if-item">
                            <p>开始页码：</p>
                            <el-input
                              size="mini"
                              v-model="input"
                              placeholder=""
                            ></el-input>
                          </div>
                          <div class="if-item">
                            <p>总页码：</p>
                            <el-input
                              size="mini"
                              v-model="input"
                              placeholder=""
                            ></el-input>
                            <p>20条/页，最多50页</p>
                          </div>
                        </div>
                        <div class="collection-item">
                          <div class="if-item">
                            <p>销量区间：</p>
                            <el-input
                              size="mini"
                              v-model="input"
                              placeholder=""
                            ></el-input
                            ><span>-</span>
                            <el-input
                              size="mini"
                              v-model="input"
                              placeholder=""
                            ></el-input>
                          </div>
                        </div>
                        <div class="collection-item">
                          <div class="if-item">
                            <p>价格区间：</p>
                            <el-input
                              size="mini"
                              v-model="input"
                              placeholder=""
                            ></el-input
                            ><span>-</span>
                            <el-input
                              size="mini"
                              v-model="input"
                              placeholder=""
                            ></el-input>
                          </div>
                        </div>
                      </div>
                      <div class="filter-key">
                        <div class="top-info">
                          <p>关键词<span class="pcolor">(一行一个)</span></p>
                        </div>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                      <div class="filter-key">
                        <div class="top-info">
                          <p>过滤关键词</p>
                        </div>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                      <div class="main-btn">
                        <el-button type="primary" size="mini"
                          >开始采集</el-button
                        >
                        <el-button type="primary" size="mini" plain
                          >取消采集</el-button
                        >
                        <el-button type="primary" size="mini"
                          >收藏产品</el-button
                        >
                        <el-button type="primary" size="mini" plain
                          >编辑上新</el-button
                        >
                        <el-button type="primary" size="mini"
                          >清理全部</el-button
                        >
                      </div>
                      <div class="carry-log">
                        <div class="top-info">
                          <p>执行日志</p>
                        </div>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                    </div>
                  </div>
                </el-tab-pane>
                <el-tab-pane label="商品链接采集" name="second">
                  <div class="link-collection">
                    <div class="mall-main">
                      <div class="link-key">
                        <p>关键词<span class="pcolor">(一行一个)</span></p>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                      <div class="main-btn">
                        <el-button type="primary" size="mini"
                          >开始采集</el-button
                        >
                        <el-button type="primary" size="mini" plain
                          >取消采集</el-button
                        >
                        <el-button type="primary" size="mini"
                          >收藏产品</el-button
                        >
                        <el-button type="primary" size="mini" plain
                          >编辑上新</el-button
                        >
                        <el-button type="primary" size="mini"
                          >清理全部</el-button
                        >
                      </div>
                      <div class="carry-log">
                        <p>执行日志</p>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                    </div>
                  </div>
                </el-tab-pane>
                <el-tab-pane label="整店采集" name="third">
                  <div class="mall-collection">
                    <div>
                      <p class="mall-name">拼多多</p>
                    </div>
                    <div class="mall-main">
                      <div class="mall-link">
                        <div class="top-info">
                          <p>
                            店铺链接<span class="pcolor"
                              >(一行一个，目前仅支持淘宝整店采集)</span
                            >
                          </p>
                        </div>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                      <div class="filter-key">
                        <div class="top-info">
                          <p>
                            过滤关键词<span class="pcolor">(一行一个)</span>
                          </p>
                        </div>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                      <div class="main-btn">
                        <el-button type="primary" size="mini"
                          >开始采集</el-button
                        >
                        <el-button type="primary" size="mini" plain
                          >取消采集</el-button
                        >
                        <el-button type="primary" size="mini"
                          >收藏产品</el-button
                        >
                        <el-button type="primary" size="mini" plain
                          >编辑上新</el-button
                        >
                        <el-button type="primary" size="mini"
                          >清理全部</el-button
                        >
                      </div>
                      <div class="carry-log">
                        <div class="top-info">
                          <p>执行日志</p>
                        </div>
                        <el-input type="textarea" v-model="desc"></el-input>
                      </div>
                    </div>
                  </div>
                </el-tab-pane>
                <div class="bottom-info">
                  <p class="pcolor">
                    温馨提示：拼多多产品加载不出来，收藏或者组装数据慢，请切换本地IP
                  </p>
                </div>
              </el-tabs>
            </div>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div class="grid-content bg-purple-dark">
          <div class="source-box">
            <div class="table-box">
              <el-table
                ref="multipleTable"
                :data="tableData"
                tooltip-effect="dark"
                style="width: 100%"
                @selection-change="handleSelectionChange"
              >
                <el-table-column type="selection" width="55"> </el-table-column>
                <el-table-column label="序号" width="120">
                  <template slot-scope="scope">{{ scope.row.date }}</template>
                </el-table-column>
                <el-table-column prop="name" label="主图" width="120">
                </el-table-column>
                <el-table-column
                  prop="address"
                  label="商品ID"
                  show-overflow-tooltip
                >
                </el-table-column>
                <el-table-column
                  prop="address"
                  label="标题"
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
                  label="销售"
                  show-overflow-tooltip
                >
                </el-table-column>
                <el-table-column
                  prop="address"
                  label="来源"
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
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      desc: '',
      value: '',
      nameoptions: {},
      input: '',
      radio: 1,
      activeName: 'first',
      activeMall: '拼多多',
      malls: ['拼多多', '淘宝', '天猫', '京东', '1688', '货老板', '多多进宝'],
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
      multipleSelection: []
    }
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event)
    },
    onMalls(name) {
      this.activeMall = name
      console.log(name)
    },
    handleSelectionChange() {}
  }
}
</script>

<style lang="less" scoped>
@import '../../assets/css/base.less';
#source-search {
  .el-row {
    margin-bottom: 20px;
    display: flex;
    flex-wrap: wrap;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .bg-purple-dark {
    background: #ffffff;
  }
  .grid-content {
    border-radius: 4px;
    .search-select {
      height: 371px;
      padding: 23px;
      .search-tabs {
        .key-collection {
          padding-left: 8px;
          .malls {
            display: flex;
            .active {
              background: @showColor;
              border: 1px solid @activeColor;
              color: #f97c28;
            }
            .malls-item {
              padding: 4px 0px;
              text-align: center;
              border-radius: 4px;
              margin-right: 10px;
              width: 82px;
              font-family: MicrosoftYaHei;
              font-size: 14px;
              font-weight: normal;
              font-stretch: normal;
              line-height: 18px;
              letter-spacing: 0px;
            }
          }
          .web-collection {
            width: 400px;
            .collection-item {
              display: flex;
              margin: 0 0 10px 0;
              span {
                line-height: 28px;
                text-align: center;
                margin: 0 10px;
              }
              .if-item {
                display: flex;
                margin-right: 10px;
              }
            }
            .el-input {
              width: 60px;
            }
            .el-select {
              width: 120px;
            }
          }
          .filter-key {
            width: 252px;
          }
        }
        .link-collection {
          display: flex;
          padding-left: 8px;
          .link-key {
            width: 600px;
          }
          .carry-log {
            width: 610px;
          }
        }
        .mall-collection {
          padding-left: 8px;
          .mall-name {
            padding: 4px 0;
            font-size: 16px;
            line-height: 23px;
            color: #333333;
          }
          .filter-key {
            width: 464px;
          }
        }
      }
    }
    .source-box {
      padding: 23px;
      .table-box {
        /deep/ .el-table th {
          background: #f5f7fa;
        }
      }
    }
  }
  .mall-link {
    width: 472px;
    margin-right: 29px;
  }
  .main-btn {
    width: 270px;
    padding: 33px 37px 0 37px;
    .el-button {
      margin: 0 16px 24px 0;
    }
  }
  .bottom-info {
    padding: 10px 0;
  }
  p {
    font-weight: normal;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 0px;
    color: #666666;
  }
  .pcolor {
    color: @activeColor;
  }
  /deep/ .el-textarea__inner {
    height: 146px;
    margin: 10px 0;
    max-height: 146px;
  }
  .mall-main {
    display: flex;
    margin-top: 15px;
    justify-content: space-between;
  }
  .carry-log {
    width: 303px;
  }
}
</style>
