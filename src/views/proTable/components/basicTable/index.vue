<template>
  <el-table
    :data="props.tableData"
    ref="tableDataRef"
    style="width: 100%"
    row-key="rowKey"
    size="small"
    :height="props.height"
    :border="true"
    :show-summary="props.isFixedFooter"
    :summary-method="getSummaries"
    @selection-change="handleSelectionChange"
    >
    <!-- 树形表格不能使用列表渲染 -->
    <!-- 不能和展开行一起使用, 且展开行优先级更高 -->
    <!-- 必须指定 row-key -->
      
    <el-table-column
      prop="" 
      label="" 
      width="50px"
      align="center"
      >
    </el-table-column>

    <el-table-column
      v-if="props.isExpand"
      type="expand" 
      label="折叠" 
      width="50px"
      align="center"
      >
      <template #default="scoped">
        <div>
          "row": {{ scoped }}
        </div>
      </template>
    </el-table-column>

    <el-table-column
      v-for="(item, index) in props.tableColumn"
      :key="index"
      :type="item.type"
      :prop="item.prop"
      :label="item.label"
      :formatter="item.formatter"
      :align="item.align"
      :min-width="item.minWidth"
      :show-overflow-tooltip="item.showOverflowTooltip"
      :fixed="item.fixed"
      :sortable="item.sortable"
      >
      <template 
        #default="scoped"
        v-if="props.isInlineEdit"
        >
        <el-input 
          v-if="item.formItem === 'input'"
          v-model="scoped.row[item.prop]" 
          style="width: 80%" 
          :placeholder="item['placeholder']" 
        >
        </el-input>
      </template>
    </el-table-column>

    <el-table-column 
      label="操作"
      align="center"
      >
      <template #default="scoped">
        <el-button
          v-for="(item, index) in props.buttonColumn" 
          :key="index"
          :type="item.type" 
          :size="item.size"
          :text="item.text"
          @click="item.method(scoped)"
          >
          {{ item.cotent }}
        </el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script setup name="BasicTable">
import { ref, reactive, onMounted, onBeforeUnmount, watch, computed, markRaw, nextTick, onActivated } from "vue";
import { ElMessage } from "element-plus";

const props = defineProps({
  tableData: {
    type: Object,
    required: true,
    default: ()=>{}
  },
  tableColumn: {
    type: Object,
    required: true,
    default: ()=>{}
  },
  buttonColumn: {
    type: Object,
    required: false,
    default: ()=>{}
  },
  isExpand: {
    type: Boolean,
    default: false,
  },
  isFixedFooter: {
    type: Boolean,
    default: false
  },
  footerFileds: {
    type: Array,
    default: ["#","#","#","#","#","#","#"]
  },
  height: {
    type: String,
    default: "500px"
  },
  isInlineEdit: {
    type: Boolean,
    default: false,
  }
})

const multipleSelection = {};
const handleSelectionChange = (val) => {
  multipleSelection.value = val;
};

const getSummaries = ()=>{
  const result = props.fixedEndRowFiled;
  return result;
};
</script>

<style>

</style>