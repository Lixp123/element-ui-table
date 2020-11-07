<template>
  <el-row>
    <el-col>
      <div class="bg-table">
        <el-table
          :data="pageType==2? pageData: dataSource"
          v-bind="$attrs"
          v-on="$listeners"
        >
        <!-- 选择框 -->
          <el-table-column
            v-if="typeAttr"
            :type="typeAttr"
            width="55">
          </el-table-column>
        <!-- 第一个在最后 -->
          <el-table-column
            label=""
            width="1px">
          </el-table-column>
          <!-- 列表插槽循环 -->
          <bg-table-column v-for="(item,key) in columns" :key="key" :children="item">
            <template v-if="item.slot" v-slot:[item.slot]="slotInfo">
              <slot  :name="item.slot"  v-bind:[item.slot]="slotInfo[item.slot]"/>
            </template>
            <template  v-for="(items,keys) in getColumnsSlot(item.children)" :keys="keys"  v-slot:[items]="slotInfo"> 
                <slot :name="items"  v-bind:[items]="slotInfo[items]"/>
            </template> 
          </bg-table-column>
        </el-table>
        <!-- 分页 -->
        <div v-if="typeof this.pagination == 'object'" class="bg-page"> 
          <div class="bg-page-total">共 {{pagination.total}} 条</div>
            <el-pagination
              @size-change="handleSizeChange"
              @current-change="handleCurrentChange"
              :current-page.sync="pagination.pageIndex"
              :page-size="10"
              layout="prev, pager, next, jumper"
              :total="pagination.total">
            </el-pagination>
          </div>
          <div v-if="pageType == 2" class="bg-page"> 
              <div class="bg-page-total">共 {{pageInfo.total}} 条</div>
              <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page.sync="pageInfo.pageIndex"
                :page-size="10"
                layout="prev, pager, next, jumper"
                :total="pageInfo.total">
              </el-pagination>
          </div>
        </div>
        
    </el-col>
  </el-row>
</template>
<!-- 列表table组件 -->
<script>
//@change分页
import bgTableColumn from './bg-table-column'
export default {
  name: "topTable",
  props: {
    typeAttr:{type :String , default : '' , required : false},//选择
    columns: {type : Array | Object , default : [] , required : true },//表头
    dataSource: {type : Array  , default : [] , required : true },//数据
    pagination:{type : Object | Boolean  , default : false , required : false },//分页
  },
  data() {
    return {
      currentPage3:3,
      pageType:1,//1后端分页，2前端分页，3不分页
      pageInfo:{//前端分页信息
        total:0,
        pageIndex:0
      },
      pageData:[],//前端分页展示数据
    };
  },
  watch:{
    dataSource: {
      handler: function (val) {
        this.getPageData(this.pageInfo.pageIndex-1)
      },
      deep: true
    },
  },
  created() {
    // 分页类型
    if(typeof this.pagination == 'object'){
      this.pageType = 1
    }else if(typeof this.pagination == 'boolean'){
      if(this.pagination){
        this.pageType = 2
        this.getPageData(0)
        this.pageInfo = {
          total:this.dataSource.length,
          pageIndex:0
        }
      }else{
        this.pageType = 3
      }
    }
  },
  methods:{
    handleSizeChange(val){

    },
    handleCurrentChange(val){
      if(this.pageType == 2){
        this.$set(this.pageInfo,'pageIndex',val)
        this.getPageData(val-1)
      }
      this.$emit('change',val)
    },
    getPageData(key){//获取前端分页，当前页数据
      let dataSource = JSON.parse(JSON.stringify(this.dataSource))//深拷贝
      let pageData =  dataSource.splice(key,10)
      this.pageData = pageData
    },
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
  },
  components:{
   'bg-table-column':bgTableColumn
  }
};
</script>

<style scoped>
.bg-table{
  background: #fff;
  box-sizing: border-box;
  padding: 5px;
}
.bg-page{
  display: flex;
  justify-content: flex-end;
  height: 50px;
  align-items: center;
}
.bg-page-total{
  font-weight: 400;
  color: #606266;
  font-size: 13px;
}
</style>
