<template>
  <div class="customers container">
    <Alert v-if="alert" :msg="alert"></Alert>
    <h1 class="page-header">用户管理系统</h1>
    <input type="text" class="form-control" placeholder="请输入要搜索的内容" v-model="search"><br>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>姓名</th>
          <th>电话</th>
          <th>邮箱</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in filterCustomers">
          <td>{{ customer.name }}</td>
          <td>{{ customer.phone }}</td>
          <td>{{ customer.email }}</td>
          <td><router-link :to="'/customer/' + customer.id" class="btn btn-default">详情</router-link></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert'
  export default {
    name: "Customers",
    data(){
      return {
        customers: [],
        alert: "",
        search: ""
      }
    },
    components: {
      Alert
    },
    methods: {
      fetchCustomers(){
        this.$http.get("http://localhost:3000/users?_sort=id&_order=desc").then((data) => {
          this.customers = data.data;
        });
      }
    },
    created(){
      if(this.$route.query.alert){
        this.alert = this.$route.query.alert;
      }
      this.fetchCustomers();
    },
    computed: {
      filterCustomers(){
        return this.customers.filter((customer) => {
          return (customer.name.match(this.search.trim()) || customer.phone.match(this.search.trim()) || customer.email.match(this.search.trim()));
        });
      }
    },
    updated(){
      this.fetchCustomers();
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
