<template>
  <div class="col-1-2">
    <div style="height: 33.33%;">
      <div class="center bg-color-black">
        <dv-border-box-13 :color="['#146199']">
          <div class="center-title">
            <div
              style="position:relative;top:20px;text-align:center;font-size:0.2rem;color:cyan;"
            >参训人员</div>
            <dv-decoration-5 style="width:50%;height:40px;margin:0 auto;" />
          </div>
          <div class="percent">
            <div class="item">
              <span>{{ rate[0].id }}</span>
              <centerChart
                :id="rate[0].id"
                :tips="rate[0].tips"
                :colorObj="rate[0].colorData"
                ref="centerChart1"
              />
            </div>
            <div class="item text">
              <p class="describe">参训数量 98 万次</p>
              <p class="describe">去年参训 80 万次</p>
              <p class="describe">同比增长 {{ Math.round(((98 - 80) / 80) * 100) }}%</p>
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
             <div class="item text">
              <p class="describe">参训率 99%</p>
              <p class="describe">去年参训率 95%</p>
              <p class="describe">同比增长 {{ Math.round(((99 - 95) / 95) * 100) }}%</p>
            </div>
          </div>
        </dv-border-box-13>
      </div>
    </div>
   <div style="height: 33.33%;">
      <div class="center bg-color-black">
        <dv-border-box-13 :color="['#146199']">
          <div class="center-title">
            <div
              style="position:relative;top:20px;text-align:center;font-size:0.2rem;color:cyan;"
            >参训装备</div>
            <dv-decoration-5 style="width:50%;height:40px;margin:0 auto;" />
          </div>
          <bottomLeftChart style="float:left;width:100%;height:100%;"></bottomLeftChart>
        </dv-border-box-13>
      </div>
    </div>
    <div style="height: 33.33%;">
      <div class="center bg-color-black">
        <dv-border-box-13 :color="['#146199']">
          <div class="center-title">
            <div
              style="position:relative;top:20px;text-align:center;font-size:0.2rem;color:cyan;"
            >物资器材</div>
            <dv-decoration-5 style="width:50%;height:40px;margin:0 auto;" />
          </div>
          <wuziqicai></wuziqicai>
        </dv-border-box-13>
      </div>
    </div>
  </div>
</template>
 
<script>
import bottomLeftChart from "@/components/echart/bottom/bottomLeftChart";
import centerChart from "@/components/echart/center/centerChartRate";
import wuziqicai from "@/components/echart/wuziqicaiChart.vue";
export default {
  data() {
    return {
      titleItem: [
        {
          title: "今年累计训练次数",
          number: {
            number: [120],
            toFixed: 1,
            content: "{nt}",
            style: {
              fontSize: 15,
              fill: "#3de7c9"
            }
          }
        },
        {
          title: "本月累计训练次数",
          number: {
            number: [18],
            toFixed: 1,
            content: "{nt}",
            style: {
              fontSize: 15,
              fill: "#3de7c9"
            }
          }
        },
        {
          title: "今日累计训练次数",
          number: {
            number: [2],
            toFixed: 1,
            content: "{nt}",
            style: {
              fontSize: 15,
              fill: "#3de7c9"
            }
          }
        },
        {
          title: "今年参训数量次数",
          number: {
            number: [14],
            toFixed: 1,
            content: "{nt}",
            style: {
              fontSize: 15,
              fill: "#3de7c9"
            }
          }
        },
        {
          title: "今年参训率次数",
          number: {
            number: [106],
            toFixed: 1,
            content: "{nt}",
            style: {
              fontSize: 15,
              fill: "#3de7c9"
            }
          }
        },
        {
          title: "今年参训率个数",
          number: {
            number: [100],
            toFixed: 1,
            content: "{nt}",

            style: {
              fontSize: 15,
              fill: "#3de7c9"
            }
          }
        }
      ],
      ranking: {
        data: [
          {
            name: "新乡",
            value: 80
          }
        ],
        waitTime: 4000,
        carousel: "single",
        unit: "件"
      },
      config: {
        header: ["单位", "数量"],
        data: [
          ['<span style="color:#9fe6b8;">海淀区政府</span>', "23"],
          ['<span style="color:#9fe6b8;">市发展改革委</span>', "26"],
          ['<span style="color:#9fe6b8;">市民政局</span>', "35"],
          ['<span style="color:#9fe6b8;">市城市管理委</span>', "39"],
          ['<span style="color:#9fe6b8;">市规划自然资源委</span>', "39"],
          ['<span style="color:#9fe6b8;">市住房城乡建设委</span>', "45"],
          ['<span style="color:#9fe6b8;">市公安局</span>', "53"],
          ['<span style="color:#9fe6b8;">市教委</span>', "55"],
          ['<span style="color:#9fe6b8;">市卫生健康委</span>', "60"],
          ['<span style="color:#9fe6b8;">市交通委</span>', "153"]
        ],
        rowNum: 5, //表格行数
        headerHeight: 35,
        headerBGC: "#0f1325", //表头
        oddRowBGC: "#0f1325", //奇数行
        evenRowBGC: "#171c33", //偶数行
        index: true,
        columnWidth: [30, 150, 50],
        align: ["center"],
        waitTime: 3000,
        carousel: "page"
      },
      water: {
        data: [5, 45],
        shape: "roundRect",
        formatter: "{value}%",
        waveNum: 3
      },
      // 通过率和达标率的组件复用数据
      rate: [
        {
          id: "参训数量",
          tips: 98,
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
          id: "参训率",
          tips: 99,
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
      

      rate2: [
        {
          id: "车辆",
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
          id: "武器",
          tips: 78,
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

      rate3: [
        {
          id: "物资",
          tips: 22,
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
          id: "器材",
          tips: 34,
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
      count: [[], [], [], []],
      contrast: [[], []],
      colors: ["cyan", "#ff5722", "#33cea0", "#1a5cd7", "cyan", "#ff5722"],
      statistics: {
        data: [],
        colors: [
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da",
          "#37a2da"
        ],
        showValue: true,
        unit: "件"
      }
    };
  },

  mounted() {
    // this.fetchProposalSubmit(); // 获取-数字板数据
    // this.fetchProposalReplace(); // 获取-代提百分比
    // this.fetchGroupSubmit();
    // // this.fetchUnitSum(); // 获取-承办单位-排行榜
    // this.setTimer();
  },
  methods: {
    setTimer() {
      this.timer = setInterval(() => {
        this.fetchProposalSubmit(); // 获取-数字板数据
        this.fetchProposalReplace(); // 获取-代提百分比
        this.fetchGroupSubmit();
        // this.fetchUnitSum(); // 获取-承办单位-排行榜
        // this.fetchState(); // 获取-状态
        // this.fetchSubjectSum(); // 获取-主题词
      }, 3000);
    },
    async fetchProposalSubmit() {
      const { data } = await this.$http.get("getDataByName?name=PROPOSAL_SUM");

      let status = data.status;
      let titleData = JSON.parse(data.data);

      var titleRes = new Array();
      if (status === 200) {
        for (var i = titleData.length - 1; i >= 0; i--) {
          var item = {
            title: "",
            number: {
              number: [],
              toFixed: 0,
              content: "{nt}",
              style: {
                fontSize: 15,
                fill: "#3de7c9"
              }
            }
          };
          item.title = titleData[i].X0;

          item.number.number.push(titleData[i].COUNT);
          titleRes.push(item);
        }
        this.titleItem = titleRes;
      }
    },
    async fetchProposalReplace() {
      const { data } = await this.$http.get("getDataByName?name=SUBMIT_SUM");
      const res = await this.$http.get("getDataByName?name=PREV_SESSION_ME");
      let status = data.status;
      let dataList = JSON.parse(data.data);
      let contrast = JSON.parse(res.data.data);
      if (status === 200) {
        this.count = [...dataList];
        this.contrast = [...contrast];
        this.rate[0].id = dataList[0].X0;
        this.rate[1].id = dataList[2].X0;
        let submitSumMe = dataList[0].COUNT + 0;
        let submitSumNotMe = dataList[2].COUNT + 0;
        let count = submitSumMe + submitSumNotMe;
        submitSumMe = parseFloat((submitSumMe / count) * 100).toFixed(2);
        submitSumNotMe = parseFloat((submitSumNotMe / count) * 100).toFixed(2);

        this.$refs.centerChart1.refresh(submitSumMe);
        this.$refs.centerChart2.refresh(submitSumNotMe);
      }
    },
    async fetchUnitSum() {
      const { data } = await this.$http.get(
        "getDataByName?name=UNIT_HANDLE_SUM"
      );

      let status = data.status;
      let dataList = JSON.parse(data.data);

      let resultList = new Array();

      if (status === 200) {
        for (var i = dataList.length - 1; i >= 0; i--) {
          var item = ["组件1", "dev-1"];
          let colorCode = "";
          if (i % 2 == 0) {
            colorCode = '<span style="color:#9fe6b8;">';
          } else {
            colorCode = '<span style="color:#67e0e3;">';
          }
          item[0] = colorCode + dataList[i].X0 + "</span>";
          item[1] = colorCode + dataList[i].COUNT + "</span>";
          resultList.push(item);
        }
        this.config.data = resultList;
        this.$refs["unit"].updateRows(resultList);
      }
    },
    async fetchState() {
      const { data } = await this.$http.get("getDataByName?name=STATE_SUM");

      let status = data.status;
      let dataList = JSON.parse(data.data);

      if (status === 200) {
        this.$refs.bottomLeftChartState.refresh(dataList);
      }
    },
    async fetchGroupSubmit() {
      const { data } = await this.$http.get("getDataByName?name=GROUP_SUM");

      let status = data.status;
      let dataList = JSON.parse(data.data);

      var resultList = new Array();
      if (status === 200) {
        var order = [
          "东城团",
          "西城团",
          "朝阳团",
          "海淀团",
          "丰台团",
          "石景山团",
          "门头沟团",
          "房山团",
          "通州团",
          "顺义团",
          "昌平团",
          "大兴团",
          "平谷团",
          "怀柔团",
          "密云团",
          "延庆团",
          "驻京部队"
        ];
        for (var i = 0; i < order.length; i++) {
          var item = { name: "怀柔区", value: 38 };
          item.name = order[i];
          var index = dataList.findIndex(v => {
            return v.X0 == item.name;
          });
          item.value = index === -1 ? 0 : dataList[index].COUNT;
          resultList.push(item);
        }
        this.statistics.data = resultList;
        this.statistics = { ...this.statistics };
      }
    }
  },
  components: {
    centerChart,
    bottomLeftChart,
    wuziqicai
    
  }
};
</script>

<style lang="scss" scoped>
.col-1-2 {
  .bg-color-black {
    background-color: rgba(19, 25, 47, 0.6);
  }
  width: 33.33%;
  display: flex;
  flex-direction: column;
  .top {
    height: 40%;
    .classify {
      padding: 0.1rem;
      width: 100%;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      overflow: hidden;
      .item {
        border-radius: 0.1rem;
        padding-top: 0.13rem;
        margin-top: 0.2rem;
        width: 30%;
        height: 0.75rem;
        font-size: 0.185rem;
      }
    }
  }
  .center {
    height: 100%;
    .border-box-content {
      display: flex;
      flex-direction: column;
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
  .bottom-label {
      position: relative;
      top: 0.2rem;
      left: 0.2rem;
    }
  .bottom {
    flex-grow: 1;
    padding: 0 0.05rem;
    padding-bottom: 0;
    width: 100%;
    display: flex;
    height: 35%; // 3.5875rem;
    justify-content: space-between;
    .bg-color-black {
      border-radius: 0.0625rem;
    }
    .ranking {
      padding: 0.125rem;
      width: 46%;
    }
  }
}
</style>