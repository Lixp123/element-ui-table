<template>
  <div style="padding:10px 60px">
    <topTable
      :border="true"
      :columns="columns"
      :dataSource="dataSource"
      :pagination="true"
      typeAttr="selection"
      @change="onChange"
    >
      <template v-slot:open="{open}">
        {{open.sex}}
      </template>
      <template #name="{name}">
        {{name.name}}999
      </template>
    </topTable>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      pagination:{
        total:0,pageIndex:0
      },
      dataSource:[
        {on:1,grade_on:'一年级',class_on:'一班',name:'新富1',sex:'女',age:'15'},
        {on:2,grade_on:'一年级',class_on:'一班',name:'新富2',sex:'女',age:'14'},
        {on:3,grade_on:'一年级',class_on:'一班',name:'新富3',sex:'男',age:'12'},
        {on:4,grade_on:'一年级',class_on:'一班',name:'新富4',sex:'女',age:'16'},
        {on:5,grade_on:'一年级',class_on:'一班',name:'新富5',sex:'男',age:'12'},
        {on:6,grade_on:'一年级',class_on:'一班',name:'新富6',sex:'女',age:'14'},
        {on:7,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:8,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:9,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:10,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:11,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:12,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:13,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:14,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:1,grade_on:'一年级',class_on:'一班',name:'新富1',sex:'女',age:'15'},
        {on:2,grade_on:'一年级',class_on:'一班',name:'新富2',sex:'女',age:'14'},
        {on:3,grade_on:'一年级',class_on:'一班',name:'新富3',sex:'男',age:'12'},
        {on:4,grade_on:'一年级',class_on:'一班',name:'新富4',sex:'女',age:'16'},
        {on:5,grade_on:'一年级',class_on:'一班',name:'新富5',sex:'男',age:'12'},
        {on:6,grade_on:'一年级',class_on:'一班',name:'新富6',sex:'女',age:'14'},
        {on:7,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:8,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:9,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:10,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:11,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:12,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:13,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:14,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:1,grade_on:'一年级',class_on:'一班',name:'新富1',sex:'女',age:'15'},
        {on:2,grade_on:'一年级',class_on:'一班',name:'新富2',sex:'女',age:'14'},
        {on:3,grade_on:'一年级',class_on:'一班',name:'新富3',sex:'男',age:'12'},
        {on:4,grade_on:'一年级',class_on:'一班',name:'新富4',sex:'女',age:'16'},
        {on:5,grade_on:'一年级',class_on:'一班',name:'新富5',sex:'男',age:'12'},
        {on:6,grade_on:'一年级',class_on:'一班',name:'新富6',sex:'女',age:'14'},
        {on:7,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:8,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:9,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:10,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:11,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:12,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:13,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
        {on:14,grade_on:'一年级',class_on:'一班',name:'新富7',sex:'男',age:'12'},
      ],
      columns:[
        {
            title: "序号1",
            dataIndex: "on"
          },
          {
            title: "序号",
            dataIndex: "on"
          },
          {
            title: "年级",
            dataIndex: "grade_on"
          },
          {
            title: "班级",
            dataIndex: "class_on"
          },
          {
            title: "信息",
            dataIndex: "info",
            children:[
              {
                title: "姓名1",
                dataIndex: "name",
                children:[
                  {
                    title: "姓名",
                    dataIndex: "name",
                    slot:'name'
                  },
                  {
                    title: "年龄",
                    dataIndex: "age"
                  },
                ]
              },
              {
                title: "年龄",
                dataIndex: "age"
              },
            ]
          },
          {
            title: "姓别",
            dataIndex: "sex"
          },
          {
            title: "操作",
            dataIndex: "open",
            slot:'open'
          }
      ]
    }
  },
  created(){
 
  },
  methods:{
    onChange(pageIndex){

    },
    printInfo(item){
      console.log(item,775)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
