<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div id="tree" ref="tree_ref" style="width: 1000px; height: 800px"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      treeData: {
        name: "flare",
        children: [
          {
            name: "data",
            children: [
              {
                name: "converters",
                children: [
                  { name: "Converters", value: 721 },
                  { name: "DelimitedTextConverter", value: 4294 },
                ],
              },
              {
                name: "DataUtil",
                value: 3322,
              },
            ],
          },
          {
            name: "display",
            children: [
              { name: "DirtySprite", value: 8833 },
              { name: "LineSprite", value: 1732 },
              { name: "RectSprite", value: 3623 },
            ],
          },
          {
            name: "flex",
            children: [{ name: "FlareVis", value: 4116 }],
          },
          {
            name: "query",
            children: [
              { name: "AggregateExpression", value: 1616 },
              { name: "And", value: 1027 },
              { name: "Arithmetic", value: 3891 },
              { name: "Average", value: 891 },
              { name: "BinaryExpression", value: 2893 },
              { name: "Comparison", value: 5103 },
              { name: "CompositeExpression", value: 3677 },
              { name: "Count", value: 781 },
              { name: "DateUtil", value: 4141 },
              { name: "Distinct", value: 933 },
              { name: "Expression", value: 5130 },
              { name: "ExpressionIterator", value: 3617 },
              { name: "Fn", value: 3240 },
              { name: "If", value: 2732 },
              { name: "IsA", value: 2039 },
              { name: "Literal", value: 1214 },
              { name: "Match", value: 3748 },
              { name: "Maximum", value: 843 },
              {
                name: "methods",
                children: [
                  { name: "add", value: 593 },
                  { name: "and", value: 330 },
                  { name: "average", value: 287 },
                  { name: "count", value: 277 },
                  { name: "distinct", value: 292 },
                  { name: "div", value: 595 },
                  { name: "eq", value: 594 },
                  { name: "fn", value: 460 },
                  { name: "gt", value: 603 },
                  { name: "gte", value: 625 },
                  { name: "iff", value: 748 },
                  { name: "isa", value: 461 },
                  { name: "lt", value: 597 },
                  { name: "lte", value: 619 },
                  { name: "max", value: 283 },
                  { name: "min", value: 283 },
                  { name: "mod", value: 591 },
                  { name: "mul", value: 603 },
                  { name: "neq", value: 599 },
                  { name: "not", value: 386 },
                  { name: "or", value: 323 },
                  { name: "orderby", value: 307 },
                  { name: "range", value: 772 },
                  { name: "select", value: 296 },
                  { name: "stddev", value: 363 },
                  { name: "sub", value: 600 },
                  { name: "sum", value: 280 },
                  { name: "update", value: 307 },
                  { name: "variance", value: 335 },
                  { name: "where", value: 299 },
                  { name: "xor", value: 354 },
                  { name: "_", value: 264 },
                ],
              },
              { name: "Minimum", value: 843 },
              { name: "Not", value: 1554 },
              { name: "Or", value: 970 },
              { name: "Query", value: 13896 },
              { name: "Range", value: 1594 },
              { name: "StringUtil", value: 4130 },
              { name: "Sum", value: 791 },
              { name: "Variable", value: 1124 },
              { name: "Variance", value: 1876 },
              { name: "Xor", value: 1101 },
            ],
          },
          {
            name: "scale",
            children: [
              { name: "IScaleMap", value: 2105 },
              { name: "LinearScale", value: 1316 },
              { name: "LogScale", value: 3151 },
              { name: "OrdinalScale", value: 3770 },
              { name: "QuantileScale", value: 2435 },
              { name: "QuantitativeScale", value: 4839 },
              { name: "RootScale", value: 1756 },
              { name: "Scale", value: 4268 },
              { name: "ScaleType", value: 1821 },
              { name: "TimeScale", value: 5833 },
            ],
          },
        ],
      },
      chartInstance: null,
    };
  },
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      this.chartInstance = this.$echarts.init(this.$refs.tree_ref);
      let option = {
        tooltip: {
          trigger: "item",
          triggerOn: "mousemove",
        },
        legend: {
          top: "2%",
          left: "3%",
          orient: "vertical",
          data: [
            {
              name: "tree1",
              icon: "rectangle",
            },
            {
              name: "tree2",
              icon: "rectangle",
            },
          ],
          borderColor: "#c23531",
        },
        series: [
          {
            type: "tree",

            name: "tree1",

            data: [this.treeData],

            top: "5%",
            left: "7%",
            bottom: "2%",
            right: "60%",

            symbolSize: 7,

            label: {
              position: "left",
              verticalAlign: "middle",
              align: "right",
            },

            leaves: {
              label: {
                position: "right",
                verticalAlign: "middle",
                align: "left",
              },
            },

            emphasis: {
              focus: "descendant",
            },

            expandAndCollapse: true,

            animationDuration: 550,
            animationDurationUpdate: 750,
          },
          {
            type: "tree",
            name: "tree2",
            data: [this.treeData],

            top: "20%",
            left: "60%",
            bottom: "22%",
            right: "18%",

            symbolSize: 7,

            label: {
              position: "left",
              verticalAlign: "middle",
              align: "right",
            },

            leaves: {
              label: {
                position: "right",
                verticalAlign: "middle",
                align: "left",
              },
            },

            expandAndCollapse: true,

            emphasis: {
              focus: "descendant",
            },

            animationDuration: 550,
            animationDurationUpdate: 750,
          },
        ],
      };
      this.chartInstance.setOption(option);
      this.chartInstance.on("click", function (parmas) {

        console.log(`----------click------------`,parmas);
        /*   myChart.setOption({
            series: [
              {
                name: "pie",
                // 通过饼图表现单个柱子中的数据分布
                data: [detail.data],
              },
            ],
          }); */
      });

      this.chartInstance.on("mouseover", function (parmas) {

        console.log(`----------mouseover------------`,parmas);
        /*   myChart.setOption({
            series: [
              {
                name: "pie",
                // 通过饼图表现单个柱子中的数据分布
                data: [detail.data],
              },
            ],
          }); */
      });
      // 图例开关的行为只会触发 legendselectchanged 事件
      this.chartInstance.on("legendselectchanged", function (params) {
        // 获取点击图例的选中状态
        var isSelected = params.selected[params.name];
        // 在控制台中打印
        console.log(
          (isSelected ? "选中了" : "取消选中了") + "图例" + params.name
        );
        // 打印所有图例的状态
        console.log(params.selected);
      });
    },
  },
};
</script>

<style scoped>
</style>
