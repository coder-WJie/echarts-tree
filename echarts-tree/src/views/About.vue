<template>
  <div class="about">
    <div class="manager">
      <el-descriptions title="仓库信息">
        <el-descriptions-item label="仓库名称"
          >kooriookami</el-descriptions-item
        >
        <el-descriptions-item label="仓库创建者"
          >kooriookami</el-descriptions-item
        >
        <el-descriptions-item label="仓库分支总数"
          >{{branchesTotal}}</el-descriptions-item
        >
        <el-descriptions-item
          label="当前分支"
          :labelStyle="{ lineHeight: '40px' }"
        >
          <el-input
            v-model="currentBranchName"
            @change="currentBranchChange"
            placeholder="请输入分支名"
          ></el-input>
        </el-descriptions-item>
        <el-descriptions-item
          label="分支展开类型"
          :labelStyle="{ lineHeight: '32px' }"
        >
          <el-radio-group v-model="exapandMethod" size="small">
            <el-radio-button label="全部展开"></el-radio-button>
            <el-radio-button label="逐级展开"></el-radio-button>
          </el-radio-group>
        </el-descriptions-item>
        <el-descriptions-item label="备注">
          <el-tag size="small">正交树图</el-tag>
        </el-descriptions-item>
        <el-descriptions-item label="提交记录">个人提交记录/仓库完整提交记录</el-descriptions-item>
        <el-descriptions-item label="其他暂定"
          >kooriookami</el-descriptions-item
        >
      </el-descriptions>
    </div>
    <!-- 树图 -->
    <div id="tree" ref="tree_ref"></div>
    <!-- commit信息 -->
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>当前分支信息</span>
        <el-button style="float: right; padding: 3px 0" type="text"
        @click="goParentBranch"
          >父级分支</el-button
        >
      </div>
      <div class="branchInfo">
        <p>分支名：{{ currentBranch.name }}</p>
        <p>分支创建者：{{ currentBranch.dataIndex }}</p>
        <p>分支贡献者：{{ currentBranch.dataIndex }}</p>
        <p>分支状态：正在开发/开发完毕</p>
        <p>最近修改：{{ currentBranch.value }}</p>
      </div>
    </el-card>
  </div>
</template>
<script>
import flatObj from '../utils/flatObject'
export default {
  data() {
    return {
      exapandMethod: "", // 展开方式
      currentBranchName: "", // 当前分支
      currentBranch: {
        name: "",
        info: {},
      },
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
  computed: {
    branchesTotal() {
      return flatObj(this.treeData).length
    }
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
            left: "17%",
            bottom: "2%",
            right: "60%",

            symbolSize: 12,
            roam: true,
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
              focus: "none",
            },

            expandAndCollapse: true,

            animationDuration: 550,
            animationDurationUpdate: 750,
          },
        ],
        dataZoom: [{}],
      };
      this.chartInstance.setOption(option);
      // 点击事件
      this.chartInstance.on("click", (parmas) => {
        console.log(`----------click------------`, parmas);
        this.currentBranchName = parmas.name; // 分支名
        this.currentBranch = parmas; // 分支信息
      });
    },
    // 搜索框搜索分支
    currentBranchChange(currentBranchName) {
      if(!currentBranchName) return
      // 拿到 分支名匹配的data，设置配置项
      let currentBranchData = flatObj(this.treeData).find(item => {
        if(item.name === currentBranchName){
        }
        return item.name === currentBranchName
      })
      this.currentBranch = currentBranchData
      console.log(`----------currentBranch------------`,currentBranchData);
       this.chartInstance.setOption({
            series: [
              {
                data: [currentBranchData],
              },
            ],
          });
    },
    // 查看当前分支的父级分支
    goParentBranch() {
      console.log(`----------展示父级分支------------`);
    }
  },
};
</script>

<style scoped>
.manager {
  /* border: 1px solid; */
  border-radius: 2px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
#tree {
  height: 800px;
  width: 800px;
  margin: 0;
  display: inline-block;
}
/deep/ .el-descriptions-item {
  /* height: 40; */
  /* line-height: 40; */
}

.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}

.box-card {
  position: absolute;
  right: 7px;
  display: inline-block;
  width: 380px;
  height: 800px;
  margin: 0px;
}
</style>
