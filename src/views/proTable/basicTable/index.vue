<template>
  <el-card>
    <ul>
      <li>
        1. 树形表格不能使用列表渲染, 必须单独使用一列表格列来表示
      </li>
      <li>
        2. 树形表格不能和展开行一起使用
      </li>
      <li>
        3. 树形表格必须指定 row-key
      </li>
      <li>
        4. 树形表格的排序, 是分层排序的
      </li>
      <li>
        5. 当 row 中包含 children 字段时，被视为树形数据
      </li>
      <li>
        6. 只有当 isFixedFooter 是否固定表尾为 true 时, footerFileds 表尾字段才会生效
      </li>
    </ul>
        
    <BasicTable
      v-model:tableData="tableData"
      v-model:tableColumn="tableColumn"
      v-model:buttonColumn="buttonColumn"
      :height="'200px'"
      :isExpand="false"
      :isInlineEdit="false"
      :isFixedFooter="false"
      :footerFileds="['','','','ANA','ANA','ANA','ANA']"
      >
    </BasicTable>
  </el-card>
</template>

<script setup name="BasicTable">
import { ref, reactive, onMounted, onBeforeUnmount, watch, computed, markRaw, nextTick, onActivated } from "vue";
import { ElMessage } from "element-plus";
import BasicTable from "../components/basicTable/index"

const tableData = reactive([
  {
    rowKey: 1,
    tree: "树形表格",
    name: "测试用例",
    date: "2024-08-01",
    age: "1",
    // children: [
    //   {
    //     rowKey: 2,
    //     tree: "树形",
    //     name: "测试用例2",
    //     date: "2024-08-02",
    //     age: "2",
    //   }
    // ]
  },
  {
    rowKey: 3,
    tree: "树形表格",
    name: "测试用例3",
    date: "2024-08-03",
    age: "3"
  }
]);
const tableColumn = reactive([
  {
    type: "selection",
    prop: "",
    label: "",
    minWidth: "",
    fixed: false,
    align: "center"
  },
  {
    type: "index",
    prop: "",
    label: "索引",
    minWidth: "",
    fixed: false,
    align: "center",
  },
  {
    type: "",
    prop: "name",
    label: "姓名",
    minWidth: "100px",
    fixed: false,
    formItem: "input",
    align: "center",
  },
  {
    type: "",
    prop: "date",
    label: "日期",
    minWidth: "100px",
    fixed: false,
    formItem: "input",
    align: "center",
    sortable: false
  },
  {
    type: "",
    prop: "age",
    label: "年龄",
    minWidth: "100px",
    fixed: false,
    formItem: "input",
    align: "center",
    sortable: false
  }
]);
const buttonColumn= [
  {
    type: "primary",
    size: "small",
    text: true,
    cotent: "操作1",
    method: (scoped)=>{
      console.log(scoped.$index);
      console.log(scoped);
      ElMessage({
        type: "success",
        message: "1"
      });
    }
  },
  {
    type: "success",
    size: "small",
    text: false,
    cotent: "操作2",
    method: (scoped)=>{
      console.log(scoped.$index);
      ElMessage({
        type: "success",
        message: "2"
      });
    }
  },
  {
    type: "info",
    size: "small",
    text: false,
    cotent: "操作3",
    method: (scoped)=>{
      console.log(scoped.$index);
      ElMessage({
        type: "success",
        message: "3"
      });
    }
  }
];

// 字符串实现表格按钮的列表渲染
// const onClickTableButton = (scoped, method)=>{
//   // 此处报错的原因是因为在 Vue3 中取消了 this， 而是改为了响应式获取。
//   // Cannot read properties of undefined (reading 'printLog')
//   // this[method](scoped);
//   // 将字符串当作函数名执行 - 方法一
//   eval(`${method}(scoped)`);
//   // 将字符串当作函数名执行 - 方法二
//   // if(method === "printLog"){
//   //   printLog(scoped);
//   // }
// };
</script>

<style lang="scss" scoped>
.el-card {
  margin: 10px 10px 10px 10px;
  border-radius: 1%;
}
</style>