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
        <!-- <div id="wc" class="wc" ref="chart"></div> -->
        <!-- <bottomLeftChartState ref="bottomLeftChartState" /> -->
        <studyChart></studyChart>
      </div>
    </div>
  </div>
  
</template>

<script>
import echarts from "echarts";
import "echarts-wordcloud";
import image from "../assets/bear.png";
import studyChart from "@/components/echart/studyChart.vue";

export default {
  data() {
    return {
      words: [],
      mycharts: null
    };
  },
  computed: {
    option: function() {
      return {
        // 设置标题，居中显示
        // title: {
        //   text: "训练热点词",
        //   left: 20,
        //   top: 20,
        //   textStyle: {
        //     fontWeight: "normal",
        //     color: "cyan"
        //   }
        // },
        // 数据可以点击
        tooltip: {},

        series: [
          {
            // maskImage: maskResource,
            // 词的类型
            type: "wordCloud",
            // 设置字符大小范围
            sizeRange: [6, 40],
            rotationRange: [-45, 90],
            textStyle: {
              normal: {
                // 生成随机的字体颜色
                color: function() {
                  return (
                    "rgb(" +
                    [
                      Math.round(Math.random() * 255),
                      Math.round(Math.random() * 255),
                      Math.round(Math.random() * 255)
                    ].join(",") +
                    ")"
                  );
                }
              }
            },
            //不要忘记调用数据
            data: [
            {
              name:'视频',
              value:'550'
            },
            {
              name:'文档',
              value:'550'
            },
            {
              name:'系统',
              value:'550'
            },
            {
              name:'书籍',
              value:'550'
            },
            {
              name:'会议',
              value:'550'
            },
            {
              name:'讨论',
              value:'550'
            }
            
          ]
          }
        ]
      };
    }
  },
  components: {studyChart},
  mounted() {
    let maskResource = new Image();
    maskResource.src = image;
    const option = this.option;
    maskResource.onload = () => {
      const mycharts = echarts.init(document.getElementById("wc"));
      this.mycharts = mycharts;
      mycharts.setOption(option);
      mycharts.resize();
    };
    // setInterval(() => {
    //   this.fetchSubjectSum();
    // }, 3000);
  },
  methods: {
  }
};
</script>

<style lang="scss">
.fs-xl{
 font-size:16px !important
}
.wc {
  width: 100%;
  height: 100%;
}
</style>