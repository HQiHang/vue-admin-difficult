<template>
  <div class="alert">
    <div class="alert alert-warning alert-dismissible" role="alert">
      <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
      {{ msg }}
    </div>
  </div>
</template>

<script>
  export default {
    name: "Alert",
    props: ["msg"]
  }
</script>

<style scoped>

</style>
