<template>
  <div>
    <div id="centreLeft1Chart" style="width:100%; height: 100%;"></div>
  </div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";

export default {
  data() {
    return {
      chart: null,
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      // 基于准备好的dom，初始化echarts实例
      this.chart = this.$echarts.init(
        document.getElementById("centreLeft1Chart")
      );
      //  ----------------------------------------------------------------

      this.chart.setOption({
        color: [
          "#37a2da",
          "#32c5e9",
          "#9fe6b8",
          "#ffdb5c",
          "#ff9f7f",
          "#fb7293",
          "#e7bcf3",
          "#8378ea",
        ],
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)",
        },
        toolbox: {
          show: true,
        },
        calculable: true,
        legend: {
          orient: "horizontal",
          icon: "circle",
          top: 40,
          x: "center",
          data: ["一级装备", "二级装备", "三级装备", "四级装备", "五级装备", "六级装备"],
          textStyle: {
            color: "#fff",
          },
        },
        series: [
          {
            name: "参训装备分布表",
            type: "pie",
            radius: [10, 120],
            roseType: "area",
            center: ["50%", "50%"],
            data: [
              { value: 10, name: "一级装备" },
              { value: 5, name: "二级装备" },
              { value: 15, name: "三级装备" },
              { value: 25, name: "四级装备" },
              { value: 20, name: "五级装备" },
              { value: 35, name: "六级装备" },
            ],
          },
        ],
      });
    },
    refresh(data) {
      let option = this.chart.getOption();
      var resultList = new Array();
      for (let index = 0; index < data.length; index++) {
        const element = data[index];
        var item = { value: 10, name: "一级装备" };
        item.value = element.COUNT;
        item.name = element.X0;
        resultList.push(item);
      }
      option.series[0].data = resultList;
      this.chart.setOption(option);
    },
  },
  destroyed() {
    window.onresize = null;
  },
};
</script>

<style lang="scss" scoped>
</style>