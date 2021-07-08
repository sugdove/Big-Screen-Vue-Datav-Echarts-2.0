<template>
  <div id="centreRight1">
    <div class="bg-color-black">
      <div class="d-flex pt-2 pl-2">
        <span style="color: #5cd9e8">
          <icon name="chart-line"></icon>
        </span>
        <div class="d-flex">
          <span class="fs-xl text mx-2">参训装备</span>
        </div>
      </div>
      <div >
          <barChart id="test1" ref="unit" :chartStyle="{width:'100%',height:'400px'}"/>
      </div>
    </div>
  </div>
</template>

<script>
import barChart from '@/components/echart/centerLeft2/barChart' 
export default {
  data() {
    return {
     
    };
  },
  components: {barChart},
  mounted() {
    // this.fetchProposalSubmit();
    // this.changeTiming();
  },
  methods: {
    changeTiming() {
      setInterval(() => {
        this.fetchProposalSubmit(); //获取-建议情况
      }, 60000);
    },
    async fetchProposalSubmit() {
      const { data } = await this.$http.get("getDataByName?name=LOGIN_LOG");

      let status = data.status;
      let dataList = JSON.parse(data.data);

      var dataArr = new Array();
      if (status === 200) {
        for (var i = dataList.length - 1; i >= 0; i--) {
          // let item = new Array();
          // item.push(dataList[i].NAME);
          // item.push(dataList[i].TIME);
          // item.push(
          //   "<span  class='colorGrass'>" + dataList[i].MESSAGE + "</span>"
          // );
          let item = new Array();
          let colorCode = "";
          if (i % 2 == 0) {
            colorCode = '<span style="color:#78cecd;">';
          } else {
            colorCode = '<span style="color:#33cea0;">';
          }
          item[0] = colorCode + dataList[i].NAME + "</span>";
          item[1] = colorCode + dataList[i].MESSAGE + "</span>";
          dataArr.push(item);
        }
        this.config.data = dataArr;
        this.config = { ...this.config };
        // this.$refs["log"].updateRows(dataArr);
      }
    }
  }
};
</script>

<style lang="scss">
#centreRight1 {
  padding: 0.2rem;
  min-width: 3.75rem;
  border-radius: 0.0625rem;
  .bg-color-black {
    height: 4.8125rem;
    border-radius: 0.125rem;
  }
  .text {
    color: #c3cbde;
  }
  .body-box {
    border-radius: 0.125rem;
    overflow: hidden;
  }
   .barTitle{
    width: 50%;
    float: left;
    text-align: center;
    font-size: 18px;
    color: cyan;
  }
}
</style>