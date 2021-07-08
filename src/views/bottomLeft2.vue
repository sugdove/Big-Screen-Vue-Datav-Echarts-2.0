<template>
  <div id="bottomLeft">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span style="color: #5cd9e8">
          <icon name="align-left"></icon>
        </span>
        <div class="d-flex">
          <span class="fs-xl text mx-2">讨论交流</span>
        </div>
      </div>
      <div style="flex-grow: 1;">
        <dv-scroll-board :config="config" ref="unit" style="height:4.5rem;margin-top:0.2rem;" />
        <!-- <bottomLeftChartState ref="bottomLeftChartState" /> -->
      </div>
    </div>
  </div>
</template>

<script>
// import bottomLeftChartState from "@/components/echart/bottom/bottomLeftChartState";
export default {
  data() {
    return {
      config: {
        data: [
          ['<span style="color:#9fe6b8;">装备专题讨论</span>'],
          ['<span style="color:#9fe6b8;">器械专题讨论</span>'],
          ['<span style="color:#9fe6b8;">体能训练专题讨论</span>'],
          ['<span style="color:#9fe6b8;">团队训练专题讨论</span>'],
          ['<span style="color:#9fe6b8;">体能训练线上交流会</span>'],
          ['<span style="color:#9fe6b8;">团队训练线下交流会</span>'],
          ['<span style="color:#9fe6b8;">小组训练纪要</span>'],
          ['<span style="color:#9fe6b8;">团队训练纪要</span>'],
    
      
        ],
        rowNum: 10, //表格行数
        headerHeight: 35,
        headerBGC: "#0f1325", //表头
        oddRowBGC: "#0f1325", //奇数行
        evenRowBGC: "#171c33", //偶数行
        index: true,
        columnWidth: [50, 200],
        align: ["center"],
        waitTime: 3000,
        carousel: "page"
      }
    };
  },
  components: {
    
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

<style lang="scss">
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
}
</style>