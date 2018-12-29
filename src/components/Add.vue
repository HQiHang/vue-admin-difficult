<template>
  <div class="add container">
    <Alert v-if="alert" :msg="alert"></Alert>
    <h1 class="page-header">添加用户</h1>
    <form @submit.prevent="addCustomer()">
      <div class="well">
        <h4>用户信息</h4>
        <div class="form-group">
          <label>姓名</label>
          <input type="text" class="form-control" placeholder="请输入姓名" v-model="customer.name">
        </div>
        <div class="form-group">
          <label>电话</label>
          <input type="text" class="form-control" placeholder="请输入电话" v-model="customer.phone">
        </div>
        <div class="form-group">
          <label>邮箱</label>
          <input type="text" class="form-control" placeholder="请输入邮箱" v-model="customer.email">
        </div>
        <div class="form-group">
          <label>学历</label>
          <input type="text" class="form-control" placeholder="请输入学历" v-model="customer.education">
        </div>
        <div class="form-group">
          <label>职业</label>
          <input type="text" class="form-control" placeholder="请输入职业" v-model="customer.profession">
        </div>
        <div class="form-group">
          <label>简介</label>
          <textarea rows="10" class="form-control" placeholder="请输入简介" v-model="customer.profile"></textarea>
        </div>
        <button type="submit" class="btn btn-primary">确定</button>
      </div>
    </form>
  </div>
</template>

<script>
  import Alert from './Alert'
  export default {
    name: "Add",
    data(){
      return {
        customer: {},
        alert: ""
      }
    },
    components: {
      Alert
    },
    methods: {
      addCustomer(){
        if(!this.customer.name || !this.customer.phone || !this.customer.email){
          if(!this.customer.name){
            this.alert = "请输入姓名！";
            return false;
          }else if(!this.customer.phone){
            this.alert = "请输入电话！";
            return false;
          }else if(!this.customer.email){
            this.alert = "请输入邮箱！";
            return false;
          }
        }else{
          if (!(/^1[3|4|5|8][0-9]\d{8}$/).test(this.customer.phone) && this.customer.phone !== "") {
            this.alert = "请输入正确的电话！";
            return false;
          }else if(!(/^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/).test(this.customer.email) && this.customer.email !== ""){
            this.alert = "请输入正确的邮箱！";
            return false;
          }else{
            let newCustomer = {
              name: this.customer.name,
              phone: this.customer.phone,
              email: this.customer.email,
              education: this.customer.education,
              profession: this.customer.profession,
              profile: this.customer.profile,
            };
            this.$http.post("http://localhost:3000/users", newCustomer).then(() => {
              this.$router.push({ path: "/", query: { alert: "添加用户信息成功！" }});
            });
          }
        }
      }
    }
  }
</script>

<style scoped>
  .page-header {
    padding-bottom: 9px;
    margin: 20px 0 20px;
    border-bottom: 1px solid #eee;
  }
</style>
