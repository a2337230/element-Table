<template>
  <div class="search-box">
    <el-input
      v-model="input"
      placeholder="请输入人员名称查询"
      size="small"
      style="margin-right: 8px"
    ></el-input>
    <el-button
      type="primary"
      size="small"
      @click="searchData"
    >
    <i class="el-icon-search icon"></i>查询</el-button>
  </div>
</template>
<script>
export default {
  name: 'SearchBox',
  data () {
    return {
      input: ''
    }
  },
  methods: {
    searchData () {
      this.$emit('searchData', this.input)
    }
  }
}
</script>
<style scoped>
.search-box {
  display: flex;
}
.icon {
  font-weight: bold;
  margin-right: 5px;
}
</style>
