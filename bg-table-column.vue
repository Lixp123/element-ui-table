<template>
<span >
  <!-- 头部循环 -->
    <el-table-column  v-if="children.children && children.children.length>0" :label="children.title" >
        <bg-table-column v-for="(item,key) in children.children" :key="key" :children="item">
          <template v-if="item.slot" v-slot:[item.slot]="slotInfo">
              <slot  :name="item.slot"  v-bind:[item.slot]="slotInfo[item.slot]"/>
            </template>
          <template  v-for="(items,keys) in getColumnsSlot(item.children)" :keys="keys"  v-slot:[items]="slotInfo"> 
                <slot :name="items"  v-bind:[items]="slotInfo[items]"/>
          </template>
        </bg-table-column>
    </el-table-column>
    <!-- 没有子元素的column -->
    <el-table-column
      v-if="!(children.children && children.children.length>0)"
      :prop="children.dataIndex"
      v-bind="children"
      :label="children.title"
      :width="children.width || 'auto'">
        <template slot-scope="scope">
              <div>
                <div v-if="children.slot" > <slot :name="children.slot"  v-bind:[children.slot]="scope.row"/></div>
                <div v-if="!children.slot"> {{ scope.row[children.dataIndex] }}</div>
              </div>
        </template>
    </el-table-column>
</span>
</template>
<!-- 列表table组件 -->
<script>
//@Change分页
import bgTableColumn from './bg-table-column'
export default {
  components:{
   'bg-table-column':bgTableColumn
  },
  name: "bg-table-column",
  props: {
    children: {type :  Object , default : [] , required : true },//表头
  },
  data() {
    return {
   
    };
  },
  watch:{
    
  },
  created() {

  },
  methods:{
    getColumnsSlot(columns=[]){//获取插槽数据
      let slots = []
      columns.forEach(item=>{
        if(item.slot && !item.children){
          slots.push(item.slot)
        }
        if(item.children && item.children.length>0){
         slots = [...slots,...this.getColumnsSlot(item.children)] 
        }
      })
      return slots || []
    }
  }
};
</script>

<style scoped>

</style>
