<template>
  <div class="customerdetail container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h1 class="page-header">
      <span class="glyphicon glyphicon-user"> {{ customers.name }}</span>
      <span class="pull-right">
        <router-link class="btn btn-success" :to="'/edit/' + id">编辑</router-link>
        <button class="btn btn-danger" @click="deleteCustomer()">删除</button>
      </span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-phone"> {{ customers.phone }}</span></li>
      <li class="list-group-item"><span class="glyphicon glyphicon-envelope"> {{ customers.email }}</span></li>
      <li class="list-group-item"><span class="glyphicon glyphicon-home"> {{ customers.education }}</span></li>
      <li class="list-group-item"><span class="glyphicon glyphicon-asterisk"> {{ customers.profession }}</span></li>
      <li class="list-group-item"><span class="glyphicon glyphicon-tag"> {{ customers.profile }}</span></li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: "CustomerDetail",
    data(){
      return {
        id: this.$route.params.id,
        customers: {}
      }
    },
    methods: {
      fetchCustomer(){
        this.$http.get("http://localhost:3000/users/"+ this.id +"").then((data) => {
          this.customers = data.data;
        });
      },
      deleteCustomer(){
        this.$http.delete("http://localhost:3000/users/"+ this.id +"").then(() => {
          this.$router.push({ path: "/", query: { alert: "删除用户信息成功！" } });
        });
      }
    },
    created(){
      this.fetchCustomer();
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
