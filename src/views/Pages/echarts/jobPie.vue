<template>
  <div>
    <div id="main" style="width: 100%; height: 500px"></div>
  </div>
</template>

<script>
import { getJobTypeNum } from "../../../request/api";
import echarts from "echarts";
export default {
  name: "jobPie",
  data() {
    return {
      list: [],
    };
  },
  mounted: function () {
      this.getJobTypeNum();
  },
  methods: {
    getJobTypeNum() {
      getJobTypeNum({})
      .then((res) => {
          this.list = res.data;
      // 绘制图表
      var myChart = echarts.init(document.getElementById("main"));
      // 指定图表的配置项和数据
      var option = {
        backgroundColor: "#45515a",
        color: ['#ff7d27','#228b22','#57a2fd', '#47b73d', '#fcc36e', '#e4590d', '#ffb400', '#5ad01c', ],
        //标题
        title: {
          text: "职位类型统计可视化",
          left: "center",
          top: 20,
          textStyle: {
            color: "yellow",
            fontStyle: "italic", //标题字体
          },
        },
        // stillShowZeroSum: true,
        //鼠标划过时饼状图上显示的数据
        tooltip: {
          trigger: "item",
          formatter: "{a}<br/>{b}:{c} ({d}%)",
        },
        //图例
        legend: {
         
          orient: "horizontal",
          bottom:10,
          textStyle: {
            color: "white",
          },
        },
        //饼图中各模块的颜色
         toolbox: {
          show: true, //显示工具箱
          feature: {
            dataView: { show: true }, //以文字形式显示数据
            restore: { show: true }, //还原
            //dataZoom:{show:true}, //区域缩放
            saveAsImage: { show: true }, //保存图片
            //magicType:{type:['line','bar']}//动态数据切换，数据显示可以在该规定内容中切换显示方式，
          },
        },
        //  visualMap: {
        //   show: false,
        //   min: 1,
        //   max: 20,
        //   realtime: true,
        //   dimension: 2, 
        //   inRange: {
        //     //选定了要映射的对象，用inRange详细写要渲染的具体细节，[x，y]中x指最小值对应的量（亮度，饱和度等），y指最大值对应的量，其余的按各自value线性渲染
        //     color:"#b6a2de"
        //     // colorSaturation: [0, 1],
        //   },
        // },
        // 饼图数据
        series: {
          name: '职位类型信息',
          type: "pie", //echarts图的类型   pie代表饼图
          radius: "55%", //饼图中饼状部分的大小所占整个父元素的百分比
          center: ["50%", "50%"], //整个饼图在整个父元素中的位置
          roseType: "radius", //角度和半径展现百分比，'area'只用半径展现
             //饼图数据
          data: this.list,
          label: {
              //饼图图形的文本标签
              normal: {
                //下同，normal指在普通情况下样式，而非高亮时样式
                textStyle: {
                  color: "white",
                },
              },
            },
             labelLine: {
              //引导线样式
              normal: {
                lineStyle: {
                  color: "rgba(255, 255, 255, 0.3)",
                },
                smooth: 0.2, //0-1，越大越平滑弯曲
                length: 10, //从块到文字的第一段长
                length2: 20, //拐弯到文字的段长
              },
            },
          itemStyle: {
             normal: {
                   
                // color: "purple",
                shadowBlur: 200, //阴影模糊程度
                shadowColor: "rgba(0, 0, 0, 0.5)", //阴影颜色，一般黑
              },
               animationType: "scale", //初始动画效果，scale是缩放，expansion是展开
            animationEasing: "elasticOut", //初始动画缓动效果
            animationDelay: function () {
              return Math.random() * 200;
            },
          },
        },
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
       })
        .catch(function (err) {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped>
</style>

