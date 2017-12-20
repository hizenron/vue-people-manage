<template>
  <div class="manage tc">
    <button @click="add">新增</button>
    <div class="input-area" v-show="showAdd">
      <input type="text" placeholder="请输入人员姓名" v-model="nameValue">
      <button @click="addName">确定</button>
    </div>
    <table>
      <tr>
        <td>姓名</td>
        <td>操作</td>
      </tr>
      <tr v-for="(item,index) in peoples">
        <td>{{item.name}}</td>
        <td :id="index"><span @click="edit">编辑</span> <span @click="del">删除</span></td>
      </tr>
    </table>
    <div class="wrap" v-show="showEdit">
      <div class="content">
        <input type="text" placeholder="请输入姓名" v-model="newName">
        <button @click="cancel">取消</button>
        <button @click="editName">确定</button>
      </div>
    </div>
    <footer-nav :class="{isManage:isNowPage}"></footer-nav>
  </div>
</template>
<script>
  import footerNav from '../../components/footer.vue'
  export default {
    components: {
      footerNav
    },
    data(){
      return {
        isNowPage: true,
        showAdd: false,
        showEdit: false,
        peoples:[
          {'name':'Jack'},
          {'name':'joe'}
        ],
        nameValue:'',
        newName:'',
        editId:0
      }
    },
    methods:{
      add: function(){
        this.showAdd= ! this.showAdd;
      },
      addName: function(){
        let v=this.nameValue;
        if(v.trim() == ''){
          alert('请输入新增人员姓名');
        }else{
          let data={};
          data.name=v;
          this.peoples.push(data);
        }
      },
      del: function(e){
        let id=e.target.offsetParent.id;
        this.peoples.splice(id,1);

      },
      edit(e){
        let id = e.target.offsetParent.id;
        this.showEdit = true;
        this.editId = id;
        this.newName = this.peoples[id].name;
      },
      cancel(){
        this.showEdit = false;
      },
      editName(){
        let v = this.newName;
        if(v.trim() == ""){
          alert("请输入姓名")
        }else{
          this.peoples[this.editId].name = this.newName;
          this.showEdit = false
        }
      }
    }
  }
</script>

<style>
  .manage{padding-bottom:50px;}
  .manage >button{width:200px; height:40px; line-height:40px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
  table{width:100%; max-width:500px; margin:0 auto; margin-top:20px;}
  .input-area input{width: 200px; height: 40px; line-height:40px; margin:20px 0; outline:none; border:1px solid #333;}
  .input-area button{ width:60px; height: 40px; line-height:40px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
  th,td{width:100px;}
  tr input{width:100px; height:30px; padding-left:10px; outline:none; border:1px solid #333;}
  .wrap{display:table; position:fixed; top:0; left:0; height:100%; width:100%; background:rgba(0,0,0,.8); z-index: 10;}
  .wrap .content{display:table-cell; vertical-align:middle;}
  .wrap .content input{height: 40px; line-height: 40px; display:block; margin:0 auto; margin-bottom:10px; font-size:16px;}
  .wrap .content button{width:100px; height: 30px; line-height: 30px; background-color:#41b883; border: none; border-radius:5px; font-size:16px; color:#fff;}
</style>
