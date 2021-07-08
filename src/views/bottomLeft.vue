<template>
  <div id="bottomLeft">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span style="color: #5cd9e8">
          <icon name="align-left"></icon>
        </span>
        <div class="d-flex">
          <span class="fs-xl text mx-2">学习入口</span>
        </div>
      </div>
      <div style="flex-grow: 1;">
       <div class="percent">
            <div class="item">
              <span>{{ rate[0].id }}</span>
              <centerChart
                :id="rate[0].id"
                :tips="rate[0].tips"
                :isPercent="true"
                :colorObj="rate[0].colorData"
                ref="centerChart1"
              />
            </div>
           
            <div class="item">
              <span>{{ rate[1].id }}</span>
              <centerChart
                :id="rate[1].id"
                :tips="rate[1].tips"
                :isPercent="true"
                :colorObj="rate[1].colorData"
                ref="centerChart2"
              />
            </div>
             <div class="item">
              <span>{{ rate[2].id }}</span>
              <centerChart
                :id="rate[2].id"
                :tips="rate[2].tips"
                :isPercent="true"
                :colorObj="rate[2].colorData"
                ref="centerChart2"
              />
            </div>
          </div>
       
       
       
        <!-- <bottomLeftChartState ref="bottomLeftChartState" /> -->
      </div>
    </div>
  </div>
</template>

<script>
// import bottomLeftChartState from "@/components/echart/bottom/bottomLeftChartState";
import centerChart from "@/components/echart/center/centerChartRate";
export default {
  data() {
    return {
      rate: [
        {
          id: "视频",
          tips: 30,
          colorData: {
            textStyle: "#3fc0fb",
            series: {
              color: ["#00bcd44a", "transparent"],
              dataColor: {
                normal: "#03a9f4",
                shadowColor: "#97e2f5"
              }
            }
          }
        },
        {
          id: "文档",
          tips: 30,
          colorData: {
            textStyle: "#67e0e3",
            series: {
              color: ["#faf3a378", "transparent"],
              dataColor: {
                normal: "#ff9800",
                shadowColor: "#fcebad"
              }
            }
          }
        },
        {
          id: "系统",
          tips: 40,
          colorData: {
            textStyle: "#67e0e3",
            series: {
              color: ["#faf3a378", "transparent"],
              dataColor: {
                normal: "#ff9800",
                shadowColor: "#fcebad"
              }
            }
          }
        }
      ],
      config: {
         data: [
    {
      name: '周口',
      value: 55
    },
    {
      name: '南阳',
      value: 120
    },
    {
      name: '西峡',
      value: 78
    },
    {
      name: '驻马店',
      value: 66
    },
    {
      name: '新乡',
      value: 80
    }
  ]
      }
    };
  },
  components: {
    centerChart
    // bottomLeftChartState,
  },
  mounted() {
    // this.changeTiming();

  },
  methods: {
        changeTiming() {
      setInterval(() => {
        this.fetchSystemSum(); //获取-状态
      }, 3000);
    },
    async fetchSystemSum() {
      const { data } = await this.$http.get("getDataByName?name=GROUP_HAN_SUM");

      let status = data.status;
      let dataList = JSON.parse(data.data);

      if (status === 200) {
        this.$refs.bottomLeftChartState.refresh(dataList);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.fs-xl{
 font-size:16px !important
}
#bottomLeft {
  padding: 0.3rem 0.2rem;
  height: 100%;
  width: 100%;
  // height: 6.5rem;
  min-width: 3.75rem;
  border-radius: 0.0625rem;
  .bg-color-black {
    display: flex;
    flex-direction: column;
    height: 100%;
    // height: 6.0625rem;
    border-radius: 0.125rem;
  }
  .text {
    color: #c3cbde;
  }
  .chart-box {
    margin-top: 0.2rem;
    width: 2.125rem;
    height: 2.125rem;
    .active-ring-name {
      padding-top: 0.125rem;
    }
  }
  .percent {
      margin-top: 0.3rem;
      width: 100%;
      height: 2rem;
      display: flex;
      justify-content: space-around;
      .item {
        height: 1.5rem;
        span {
          margin-top: 0.0875rem;
          display: flex;
          justify-content: center;
        }
        .describe {
          text-align: left;
        }
      }
      .text {
        height: 1rem;
        flex-grow: 1;
        font-size: 0.125rem;
        margin-top: 30px;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        text-align: left;
        color: #fff;
      }
      .water {
        width: 100%;
      }
    }
}
</style>