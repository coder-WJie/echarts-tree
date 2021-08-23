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
        <el-descriptions-item label="仓库分支总数">{{
          branchesTotal
        }}</el-descriptions-item>
        <el-descriptions-item
          label="切换根分支"
          :labelStyle="{ lineHeight: '40px' }"
        >
          <el-select
            v-model="rootBranchName"
            filterable
            placeholder="请选择分支"
            @change="toggleRootBranch"
          >
            <el-option
              v-for="item in branchesArr"
              :key="item.name"
              :label="item.name"
              :value="item.name"
            >
            </el-option>
          </el-select>
        </el-descriptions-item>
        <el-descriptions-item
          label="搜索分支"
          :labelStyle="{ lineHeight: '40px' }"
        >
          <el-select
            v-model="currentBranchName"
            filterable
            placeholder="请选择分支"
            @change="findBranch"
          >
            <el-option
              v-for="item in branchesArr"
              :key="item.name"
              :label="item.name"
              :value="item.name"
            >
            </el-option>
          </el-select>
        </el-descriptions-item>
        <el-descriptions-item
          label="分支展开方式"
          :labelStyle="{ lineHeight: '32px' }"
        >
          <el-radio-group
            v-model="exapandMethod"
            size="small"
            @change="toggleExpandMethod"
          >
            <el-radio-button label="全部展开"></el-radio-button>
            <el-radio-button label="逐级展开"></el-radio-button>
          </el-radio-group>
        </el-descriptions-item>
        <el-descriptions-item label="备注">
          <el-tag size="small">正交树图</el-tag>
          <el-tag size="small">径向树图</el-tag>
          <el-tag size="small">缩进树图</el-tag>
        </el-descriptions-item>
        <el-descriptions-item label="提交记录"
          >个人提交记录/仓库完整提交记录</el-descriptions-item
        >
        <el-descriptions-item label="条件筛选"
          ><el-tag size="small">正交树图</el-tag>
          <el-tag size="small">径向树图</el-tag>
          <el-tag size="small">缩进树图</el-tag>
        </el-descriptions-item>
      </el-descriptions>
    </div>
    <div class="container">
      <!-- 树图 -->
      <div id="tree" ref="tree_ref"></div>
      <!-- commit信息 -->
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>当前分支信息</span>
          <el-button
            style="float: right; padding: 3px 0"
            type="text"
            @click="goParentBranch"
            >父级分支</el-button
          >
        </div>
        <div class="branchInfo">
          <p>分支名：{{ currentBranch.name }}</p>
          <p>分支创建者：{{ currentBranch.dataIndex }}</p>
          <p>分支贡献者：{{ currentBranch.dataIndex }}</p>
          <p>分支状态：正在开发/开发完毕</p>
          <p>提交记录：{{ currentBranch.value }}</p>
        </div>
      </el-card>
    </div>
  </div>
</template>
<script>
import flatObj from "../utils/flatObject";
export default {
  data() {
    return {
      exapandMethod: "逐级展开", // 展开方式
      rootBranchName: "", // 当前分支
      rootBranch: {
        name: "",
        info: {},
      },
      currentBranchName: "",
      currentBranch: {},
      treeData: {
        name: "flare",
        children: [
          {
            name: "data",
            collapsed: true,
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
                collapsed: false,
                children: [
                  {
                    name: "add",
                    value: 593,
                    collapsed: false,
                    children: [{ name: "Anddd", value: 1037 }],
                  },
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
    // 扁平化后的数组
    branchesArr() {
      return flatObj(this.treeData);
    },
    branchesTotal() {
      return flatObj(this.treeData).length;
    },
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
          ],
          borderColor: "#c23531",
        },
        series: [
          {
            type: "tree",

            name: "tree1",

            data: [this.treeData],

            top: "5%",
            left: "center",
            bottom: "2%",
            // right: "60%",

            itemStyle: {
              // 径向渐变，前三个参数分别是圆心 x, y 和半径，取值同线性渐变
              color: "skyblue",
            },

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
            selectedMode: true, // 支持多选
            // 选中状态
            select: {
              label: {
                borderWidth: 2,
                backgroundColor: "#e6e6e6",
                fontStyle: "italic",
                fontWight: "bolder",
                fontSize: 16,
                color: "blue",
              },
              itemStyle: {
                color: "blue",
              },
              lineStyle: {
                color: "#000",
              },
            },

            emphasis: {
              focus: "none",
              label: {
                backgroundColor: "#e6e6e6",
              },
            },

            expandAndCollapse: true,
            initialTreeDepth: 2,

            animationDuration: 550,
            animationDurationUpdate: 550,
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
      this.chartInstance.on("select", (parmas) => {
        console.log(`----------select------------`);
        this.currentBranchName = parmas.name; // 分支名
        this.currentBranch = parmas; // 分支信息
        console.log(`----------select------------`, this.currentBranch);
      });
    },
    // 切换根分支
    toggleRootBranch(rootBranchName) {
      if (!rootBranchName) return;
      // 拿到 分支名匹配的data，设置配置项
      let rootBranchData = flatObj(this.treeData).find((item) => {
        if (item.name === rootBranchName) {
        }
        return item.name === rootBranchName;
      });
      this.rootBranch = rootBranchData;
      console.log(`----------rootBranch------------`, rootBranchData);

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
          ],
          borderColor: "#c23531",
        },
        series: [
          {
            type: "tree",

            name: "tree1",

            data: [this.rootBranch],

            top: "5%",
            left: "center",
            bottom: "2%",
            // right: "60%",

            itemStyle: {
              // 径向渐变，前三个参数分别是圆心 x, y 和半径，取值同线性渐变
              color: "skyblue",
            },

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
            selectedMode: true, // 支持多选
            // 选中状态
            select: {
              label: {
                borderWidth: 2,
                backgroundColor: "#e6e6e6",
                fontStyle: "italic",
                fontWight: "bolder",
                fontSize: 16,
                color: "blue",
              },
              itemStyle: {
                color: "blue",
              },
              lineStyle: {
                color: "#000",
              },
            },

            emphasis: {
              focus: "none",
              label: {
                backgroundColor: "#e6e6e6",
              },
            },

            expandAndCollapse: true,
            initialTreeDepth: 2,

            animationDuration: 550,
            animationDurationUpdate: 550,
          },
        ],
      };
      // 先清空，再重新配置，还在寻求更好的解决方案（更新残留数据bug）
      this.chartInstance.setOption({}, true);
      this.chartInstance.setOption(option);
    },
    // 搜索分支
    findBranch() {
      this.chartInstance.dispatchAction({
        type: "select",
        name: this.currentBranchName,
      });
    },
    // 全部展开,选中节点的所有后代节点的collapse属性改为false
    toggleExpandMethod() {
      if (this.exapandMethod === "全部展开") {
        console.log(`----------allExpand------------`, this.currentBranch);
      } else {
        console.log(`----------stepExpand------------`);
      }
    },
    // 查看当前分支的父级分支
    goParentBranch() {
      console.log(`----------展示父级分支------------`);
    },
  },
};
</script>


<style scoped>
.manager {
  /* border: 1px solid; */
  border-radius: 2px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
.container {
  display: flex;
  justify-content: space-between;
}
#tree {
  left: 0;
  height: 800px;
  width: 1000px;
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
  right: 7px;
  display: inline-block;
  width: 380px;
  height: 800px;
  margin: 0px;
}
</style>
