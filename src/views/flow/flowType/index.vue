<template>
  <div class="app-container">

 <h3>流转-类型</h3>
 

    <div class="content_toplayout">
      <div class="search_content fl">
        <el-button type="primary" icon="el-icon-search"></el-button>
        <input type="text" class="search_content_input fl" placeholder="请输入关键字" />
      </div>
      <div class="button fr">
        <el-button type="primary" icon="el-icon-minus" @click="addInfo">添加</el-button>
        <el-button type="primary" icon="el-icon-plus">删除</el-button>
      </div>
    </div>
 
 

    <div class="table_box">
       <el-table
    ref="multipleTable"
    :data="tableData"
    tooltip-effect="dark"
    style="width: 100%"
    @selection-change="handleSelectionChange">
    <el-table-column
      type="selection"
      width="55">
    </el-table-column>
    <el-table-column
      label="ID">
     <template slot-scope="scope">{{ scope.$index+1 }}</template>
    </el-table-column>
    <el-table-column
      prop="type"
      label=" 类型">
    </el-table-column>
    <el-table-column
      prop="sort"
      label="排序">
    </el-table-column>
       <el-table-column
      prop="enable"
      label="启用">
        <template slot-scope="scope">
            <el-switch v-model="value1">
</el-switch>
          </template>
    </el-table-column>
  </el-table>


    </div>
 



 <el-dialog
      title="添加流转类型"
      :visible.sync="dialogVisible"
      width="80%"
      :before-close="handleClose"
    >


     <el-form label-width="140px"> 

  <el-row :gutter="20">
     <el-col :span="23">
          <div class="form_btn">
              <el-button type="primary" @click="comfirm" >保存</el-button>
              <el-button @click="dialogVisible = false">取消</el-button>
            </div>
       </el-col>
 </el-row>
 <el-row :gutter="20">
  <el-col :span="10">
    <el-form-item label="类型"  >
    <el-input v-model="flowInfo.type"></el-input>
  </el-form-item>
  </el-col>
  <el-col :span="13">
    <el-form-item label="排序">
    <el-input v-model="flowInfo.sort"></el-input>
  </el-form-item>
  </el-col>
</el-row>

<el-row :gutter="20">
  <el-col :span="23">
    <el-form-item label="描述" style="margin-bottom:5px">
   <el-input type="textarea" v-model="flowInfo.dsec"></el-input>
  </el-form-item>
  </el-col>
</el-row>

<el-row :gutter="20">
  <el-col :span="23">
    <el-form-item label="启用">
  <el-switch v-model="flowInfo.value1"></el-switch>
  </el-form-item>
  </el-col>
</el-row>

</el-form>

    </el-dialog>



 
  </div>

</template>


<script>
  export default {
    data() {
      return {
        dialogVisible: false, // 弹框的显示
        value1:true,
        flowInfo:{   //流转类型信息
          type: '',
          sort: '',
          dsec: '',
          value1:''
        },
        tableData: [{
          type: '流转测试',
          sort: 1,
          enable: false,  
        }],
        multipleSelection: []
      }
    },
    methods: {
      handleSelectionChange(val) {  //表头复选框按钮
        this.multipleSelection = val;
      },
     handleClose() {
     this.dialogVisible = false
    },
    comfirm(){
            if(!this.flowInfo.type){
        this.$message({
          message: '类型不能为空',
          type: 'warning'
        })
        return
      }
          if(!this.flowInfo.sort){
        this.$message({
          message: '排序不能为空',
          type: 'warning'
        })
        return
      }
        this.tableData.push(this.flowInfo)
             this.flowInfo={
        type: '',
        sort: '',
        dsec: ''
      };
         this.$message({
        message:'添加成功！',
         type: 'success'

      })

    },
      addInfo(){ //添加流转类型信息
      this.dialogVisible = true;

  
    
 
   

      }
    }
  }
</script>

<style>
.el-row { margin-bottom: 0px;}
.form_btn{ text-align: right; margin-bottom: 20px;}
.el-dialog__header{background:#2f66cc;text-align: center; }
.el-dialog__title{color: #fff; font-family:Arial, Helvetica, sans-serif;}
.el-dialog__headerbtn .el-dialog__close {color: #fff; font-size:24px ;}


</style>
