<template>
  <div class="left-tree">
    <el-tree
      :data="data"
      :props="defaultProps"
      @node-click="handleNodeClick"
      highlight-current
      class="pos-tree"
    ></el-tree>
  </div>
</template>
<script>
export default {
  name: 'tree',
  data() {
    return {
      data: [
        {
          label: '运营部',
          children: [
            {
              label: '运营部1',
              children: [
                {
                  label: '运营部1-1'
                }
              ]
            }
          ]
        },
        {
          label: '课程研发中心',
          children: [
            {
              label: '课程研发中心1',
              children: [
                {
                  label: '课程研发中心1-1'
                }
              ]
            }
          ]
        },
        {
          label: 'IT中心',
          children: [
            {
              label: '前端开发',
              children: [
                {
                  label: 'HTML'
                },
                {
                  label: 'CSS'
                },
                {
                  label: 'JS'
                }
              ]
            },
            {
              label: '移动开发',
              children: [
                {
                  label: 'H5开发'
                },
                {
                  label: '安卓开发'
                },
                {
                  label: 'IOS开发'
                }
              ]
            }
          ]
        },
        {
          label: '客服中心',
          children: [
            {
              label: '售前客服'
            },
            {
              label: '售后客服'
            }
          ]
        }
      ],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  methods: {
    handleNodeClick (val) {
      console.log(val)
    }
  }
}
</script>
<style scoped>
.left-tree {
  width: 200px;
  padding: 10px;
  border: 1px solid #d7d7d7;
}
</style>
