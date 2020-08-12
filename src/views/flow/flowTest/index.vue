<template>
  <div>
    <h3>流转测试flowTest</h3>
    <div id="table">
        <div class="add">
            <input type="text" placeholder="标题" v-model="obj.title">
            <input type="text" placeholder="发布人"  v-model="obj.user">
            <input type="date" placeholder="发布时间"  v-model="obj.dates">
            <button @click="add()">新增</button>
         
        </div>
        <table>
          <thead>
            <tr>
            <th>序号</th>
            <th>标题</th>
            <th>发布人</th>
            <th>发布时间</th>
            <th>操作</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(list,index) in lists">
              <td>{{index+1}}</td>
              <td>{{list.title}}</td>
              <td>{{list.user}}</td>
              <td>{{list.dates}}</td>
              <td>
                <span class="delete" @click="del()">删除</span>
                <span class="edit">编辑</span>
              </td>
            </tr>
          </tbody>
        </table>
    </div>
  
  </div>


</template>

<script>
export default {
  data() {
    return {//数据
     obj:{
     title:'',
     user:'',
     dates:''
     },
     lists:[{title:'标题1',user:'cmm',dates:'2020-3-7'}]
  }
  },
  methods:{
    add(){
      //必填
      if(!this.obj.title ||!this.obj.user ||!this.obj.dates) return;
      this.lists.push({
        title:this.obj.title,
        user:this.obj.user,
        dates:this.obj.dates
      });
      //清空
      this.obj={};
    },
    del(index){ //删除
      this.lists.splice(index,1)   //index位置 1个数

    }
  }
}

</script>

<style>

</style>
