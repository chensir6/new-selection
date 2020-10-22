<template>
  <div id="statistics">
    <div class="header">
      <div class="h-title">数据统计</div>
      <div class="h-img">
        <img src="../../assets/images/cut_06.png" alt="" />
        <img src="../../assets/images/cut_08.png" alt="" />
        <img src="../../assets/images/cut_10.png" alt="" />
        <img src="../../assets/images/cut_12.png" alt="" />
      </div>
    </div>
    <el-row :gutter="24">
      <el-col :span="11">
        <div class="grid-content ssgk">
          <div class="ssgk-h">
            <div class="ssgk-title">
              <span>实时概况</span>
            </div>
          </div>
          <div class="row">
            <div class="ssgk-item" v-for="item in gkList" :key="item.id">
              <div class="ssgk-img"><img :src="item.url" alt="" /></div>
              <div class="ssgk-title">
                <div class="price">{{ item.price }}</div>
                <div class="descript">{{ item.descript }}</div>
              </div>
            </div>
          </div>
        </div>
      </el-col>
      <el-col :span="13">
        <div class="grid-content ssgk">
          <div class="ssgk-h">
            <div class="ssgk-title">
              <span>预警中心</span>
            </div>
          </div>
          <div class="wranner-wrapper">
            <div class="wranner-item" v-for="item in earlyData" :key="item.id">
              <div>
                <span class="number">{{ item.number }}</span>
                <div class="descript">
                  <span>{{ item.name }}</span
                  ><img :src="item.Img" :alt="item.alt" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div class="grid-content sform">
          <el-form ref="sFormRef" :model="sForm" label-width="100px">
            <el-form-item label="请选择标签">
              <el-select v-model="sForm.region1" placeholder="全部" size="mini">
                <el-option label="区域一" value="shanghai"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="请选择店铺">
              <el-select v-model="sForm.region1" placeholder="全部" size="mini">
                <el-option label="区域一" value="shanghai"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="统计天数(天)">
              <el-select v-model="sForm.region1" placeholder="全部" size="mini">
                <el-option label="区域一" value="shanghai"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item>
              <el-button size="mini" type="primary" @click="onSearch"
                >搜索</el-button
              >
              <el-button size="mini" type="primary" plain>导出</el-button>
            </el-form-item>
          </el-form>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="24">
      <el-col :span="12">
        <div class="grid-content chart">
          <div class="ssgk-h">
            <div class="ssgk-title">
              <span>销售统计</span>
            </div>
          </div>
          <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
          <div id="chartLineBox" style="width: 723px;height: 347px;"></div>
        </div>
      </el-col>
      <el-col :span="12">
        <div class="grid-content chart">
          <div class="ssgk-h">
            <div class="ssgk-title">
              <span>拍单统计</span>
            </div>
          </div>
          <div id="chartListBox" style="width: 628px;height: 308px;"></div>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="24">
        <div class="grid-content chart">
          <div class="ssgk-h">
            <div class="ssgk-title">
              <span>售后统计</span>
            </div>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row>
      <el-col class="grid-content stable">
        <el-table :data="tableData" style="width: 100%">
          <el-table-column
            prop="date"
            label="统计日期"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="name"
            label="成交金额"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="name"
            label="成交单量"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="name"
            label="毛利"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="name"
            label="拍单金额"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="name"
            label="拍单单量"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="address"
            label="售后退款成功金额"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="address"
            label="售后退款成功单数"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="name"
            label="售后取消单数"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="address"
            label="空包数量"
            show-overflow-tooltip
          ></el-table-column>
          <el-table-column
            prop="address"
            label="空包消费总额"
            show-overflow-tooltip
          ></el-table-column>
        </el-table>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  data() {
    return {
      option: {},
      sForm: {
        region1: ''
      },
      gkList: [
        {
          id: 1,
          url: require('../../assets/images/cut_24.png'),
          price: 1000,
          descript: '成交金额(元)'
        },
        {
          id: 3,
          url: require('../../assets/images/cut_28.png'),
          price: 100,
          descript: '毛利'
        }
      ],
      messageData: [
        {
          id: 1,
          name: '成交金额（元）',
          number: 1000,
          proportion: '9.12%',
          isup: false
        },
        {
          id: 2,
          name: '成交单量',
          number: 0,
          proportion: '9.12%',
          isup: true
        },
        {
          id: 3,
          name: '成交客户数',
          number: 0,
          proportion: '9.12%',
          isup: false
        }
      ],
      earlyData: [
        {
          id: 1,
          name: '未处理异常订单',
          number: 1000,
          Img: require('../../assets/images/cut_77.png')
        },
        {
          id: 2,
          name: '催单回复率',
          number: 1000,
          Img: require('../../assets/images/cut_77.png')
        },
        {
          id: 3,
          name: '出库/揽件预警',
          number: 1000,
          Img: require('../../assets/images/cut_77.png')
        }
      ],
      tableData: [
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }
      ]
    }
  },
  methods: {
    onSearch() {}
  },
  mounted() {
    // 基于准备好的dom，初始化echarts实例
    this.chartLine = echarts.init(document.getElementById('chartLineBox'))
    this.chartLines = echarts.init(document.getElementById('chartListBox'))
    // 指定图表的配置项和数据
    this.option = {
      tooltip: {
        // 设置tip提示
        trigger: 'axis'
      },

      legend: {
        // 设置区分（哪条线属于什么）
        data: ['成交单量', '成交金额'],
        textStyle: {
          left: '100px'
        }
      },
      grid: {
        left: '0',
        containLabel: true
      },
      color: ['#666bff', '#ff671e'], // 设置区分（每条线是什么颜色，和 legend 一一对应）
      xAxis: {
        // 设置x轴
        type: 'category',
        boundaryGap: false, // 坐标轴两边不留白
        data: ['07-01', '07-02', '07-03', '07-04', '07-05 ', '07-01', '07-07'],
        nameTextStyle: {
          // 坐标轴名称的文字样式
          color: '#999',
          fontSize: 16,
          padding: [0, 0, 0, 20]
        },
        axisLine: {
          // 坐标轴轴线相关设置。
          lineStyle: {
            color: '#999'
          }
        }
      },
      yAxis: {
        name: '',
        nameTextStyle: {
          color: '#999',
          fontSize: 16,
          padding: [0, 0, 10, 0]
        },
        axisLine: {
          lineStyle: {
            color: '#999'
          }
        },
        type: 'value'
      },
      series: [
        {
          name: '成交单量',
          data: [
            ['07-01', 61],
            ['07-02', 33],
            ['07-03', 27],
            ['07-04', 42],
            ['07-05', 21],
            ['07-06', 17],
            ['07-07', 39]
          ],
          type: 'line', // 类型为折线图
          smooth: true,
          lineStyle: {
            // 线条样式 => 必须使用normal属性
            normal: {
              color: '#666bff'
            }
          }
        },
        {
          name: '成交金额',
          data: [
            ['07-01', 5],
            ['07-02', 23],
            ['07-03', 15],
            ['07-03', 42],
            ['07-05', 32],
            ['07-05', 27],
            ['07-07', 53]
          ],
          type: 'line', // 类型为折线图
          smooth: true,
          lineStyle: {
            // 线条样式 => 必须使用normal属性
            normal: {
              color: '#ff671e'
            }
          }
        }
      ]
    }
    // 使用刚指定的配置项和数据显示图表。
    this.chartLine.setOption(this.option)
    this.chartLines.setOption(this.option)
  }
}
</script>

<style lang="less" scoped>
#statistics {
  width: 1650px;
  padding: 24px 32px 24px 24px;
  .el-row {
    margin-bottom: 24px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .grid-content {
    border-radius: 10px;
    min-height: 36px;
    background-color: #fff;
  }
  .header {
    width: 100%;
    height: 76px;
    padding: 9px 0 41px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .h-title {
      font-size: 16px;
      font-weight: normal;
      font-stretch: normal;
      line-height: 23px;
      letter-spacing: 1px;
      color: #1a1a1a;
      font-weight: bold;
    }
    .h-img {
      display: flex;
      img {
        margin-left: 60px;
        cursor: pointer;
      }
    }
  }
  .ssgk {
    height: 206px;
    padding: 32px;
    .row {
      width: 100%;
      display: flex;
      justify-content: space-between;
      .ssgk-item {
        width: 308px;
        height: 102px;
        background-color: #fdf9f3;
        border-radius: 10px;
        position: relative;
        img {
          height: 102px;
        }
        .ssgk-title {
          position: absolute;
          left: 15px;
          bottom: 15px;
          .price {
            font-size: 20px;
            line-height: 23px;
            letter-spacing: 0px;
            color: #1a1a1a;
          }
          .descript {
            font-size: 12px;
            line-height: 23px;
            letter-spacing: 1px;
            color: #666666;
          }
        }
      }
    }
    .wranner-wrapper {
      display: flex;
      .wranner-item {
        padding: 31px 32px;
        width: 256px;
        height: 102px;
        border-radius: 10px;
        border: solid 1px #dbdbdb;
        margin-right: 17px;
        transition: all 0.3s;
        &:hover {
          box-shadow: 0 0 4px rgba(0, 0, 0, 0.2);
          transform: translateY(-3px);
        }
        .number {
          font-size: 20px;
          letter-spacing: 0px;
          color: #1a1a1a;
        }
        .descript {
          margin: 10px 0px;
          display: flex;
          justify-content: space-between;
        }
      }
    }
  }
  .sform {
    height: 92px;
    padding: 26px;
    .el-form {
      display: flex;
      margin-right: 50px;
      /deep/ .el-select .el-input__inner {
        width: 130px;
      }
      .el-button {
        margin-right: 16px;
      }
    }
  }
  .stable {
    padding: 32px;
    /deep/ .el-table th {
      background: #f5f7fa;
    }
  }
  .chart {
    height: 464px;
    padding: 32px;
  }
  .ssgk-h {
    padding-bottom: 23px;
  }
  .ssgk-title {
    font-size: 16px;
    font-weight: normal;
    font-stretch: normal;
    line-height: 23px;
    letter-spacing: 1px;
    color: #1a1a1a;
    font-weight: bold;
  }
}
</style>
