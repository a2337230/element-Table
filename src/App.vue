<template>
  <div id="app">
    <tl-table :table="dataTable" @changeSwitch="changeSwitch" @handleEdit="handleEdit">
      <template slot-scope="props" slot="username">
        <el-switch
          class="switchStyle"
          v-model="props.obj.row.switchVal"
          active-color="#1890ff"
          inactive-color="#d9d9d9"
          :active-value="1"
          :inactive-value="0"
          @change="changeSwitch(props.obj.row)"
        >
        </el-switch>
        <span style="padding-left: 5px">{{props.obj.row.switchVal?"正常":"冻结"}}</span>
      </template>
      <template slot-scope="scope" slot="examine">
        <el-select v-model="scope.obj.row.option" placeholder="请选择部门" size="small">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          >
          </el-option>
        </el-select>
      </template>
    </tl-table>
    <!-- 树形菜单 -->
    <div class="tree-menu">
      <tree-menu></tree-menu>
    </div>
    <div class="tree-menu">
      <add-btn @click.native="btnClick"></add-btn>
    </div>
    <div class="tree-menu">
      <search-box @searchData="searchData"></search-box>
    </div>
    <div class="tree-menu">
      <go-back></go-back>
    </div>
    <div class="tabs">
      <tabs :tabs="tabs"></tabs>
    </div>
    <div class="deldialog">
      <el-button type="success" @click="delDialog=true">删除数据</el-button>
      <del-dialog v-if="delDialog" @closeDialog="closeDialog" :title="delTitle" :icon="icon"></del-dialog>
    </div>
    <div class="psddialog" style="padding-top: 10px">
      <el-button type="success" @click="dialogPassword=true">重置密码</el-button>
      <psd-dialog
        v-if="dialogPassword"
        :userInfo="resetInfo"
        @closeDialog="closePsdDialog"
      ></psd-dialog>
    </div>
  </div>
</template>

<script>
import tlTable from '@/components/Table'
import TreeMenu from './components/Tree'
import AddBtn from './components/AddBtn'
import SearchBox from './components/SearchBox'
import GoBack from './components/GoBack'
import Tabs from './components/Tabs'
import DelDialog from './components/DelDialog'
import PsdDialog from './components/PsdDialog'
export default {
  name: 'App',
  data () {
    return {
      dataTable: {
        border: true,
        hasOperation: true,
        tr: [
          {
            id: '1',
            label: '序号',
            prop: 'id',
            minWidth: '100'
          },
          {
            id: '2',
            label: '姓名',
            prop: 'name'
          },
          {
            id: '3',
            label: '部门',
            prop: 'dep'
          },
          {
            id: '11',
            label: '创建时间',
            prop: 'startTime',
            sort: true,
            minWidth: '140'
          },
          {
            id: '7',
            label: '最后登录时间',
            prop: 'endTime',
            sort: true,
            minWidth: '140'
          },
          {
            id: '8',
            label: '状态',
            prop: 'username',
            show: 'template',
            minWidth: '120'
          },
          {
            id: '9',
            label: '审核',
            prop: 'examine',
            show: 'template',
            minWidth: '120'
          }
        ],
        data: [
          {
            id: 1,
            name: '张三',
            dep: '营销部',
            startTime: '2019-04-25',
            endTime: '2019-04-26',
            switchVal: 0,
            option: '未审核'
          },
          {
            id: 2,
            name: '李四',
            dep: 'IT中心',
            startTime: '2019-04-26',
            endTime: '2019-04-27',
            switchVal: 1,
            option: '已审核'
          }
        ],
        operation: { // 操作功能
          label: '操作', // 操作列的行首文字
          width: '350', // 操作列的宽度
          className: '', // 操作列的class名
          data: [ // 操作列数据
            {
              label: '默认', // 按钮文字
              Fun: 'handleEdit', // 点击按钮后触发的父组件事件
              size: 'mini', // 按钮大小
              id: '1', // 按钮循环组件的key值
              classname: 'show' // 按钮的类名
            },
            {
              label: '主要', // 按钮文字
              Fun: 'handleSubmit', // 点击按钮后触发的父组件事件
              size: 'mini', // 按钮大小
              id: '2', // 按钮循环组件的key值
              classname: 'show', // 按钮的类名
              type: 'success'
            },
            {
              label: '警告', // 按钮文字
              Fun: 'handleSubmit', // 点击按钮后触发的父组件事件
              size: 'mini', // 按钮大小
              id: '3', // 按钮循环组件的key值
              classname: 'show', // 按钮的类名
              type: 'warning'
            },
            {
              label: '危险', // 按钮文字
              Fun: 'handleSubmit', // 点击按钮后触发的父组件事件
              size: 'mini', // 按钮大小
              id: '4', // 按钮循环组件的key值
              classname: 'show', // 按钮的类名
              type: 'danger'
            },
            {
              label: '信息', // 按钮文字
              Fun: 'handleSubmit', // 点击按钮后触发的父组件事件
              size: 'mini', // 按钮大小
              id: '5', // 按钮循环组件的key值
              classname: 'show', // 按钮的类名
              type: 'info'
            }
          ]
        }
      },
      options: [{
        value: '未审核',
        label: '未审核'
      }, {
        value: '已审核',
        label: '已审核'
      }],
      value: '未审核',
      tabs: ['全部', '人员', '岗位', '已上架', '待上架', '已审核', '未审核', '未通过', '正常', '冻结'],
      delDialog: false,
      dialogPassword: false,
      delTitle: '删除',
      icon: 'el-icon-warning'
    }
  },
  methods: {
    changeSwitch (val) {
      console.log(val)
    },
    handleEdit (val) {
      console.log(val)
    },
    changeOption (val) {
      console.log(val)
    },
    btnClick () {
      alert('按钮已点击')
    },
    // 搜索框
    searchData (val) {
      console.log(val)
    },
    closeDialog (val) {
      this.delDialog = val
    },
    closePsdDialog (val) {
      this.dialogPassword = val
    }
  },
  components: {
    tlTable,
    TreeMenu,
    AddBtn,
    SearchBox,
    GoBack,
    Tabs,
    DelDialog,
    PsdDialog
  }
}
</script>

<style>
.tree-menu {
  padding-top: 20px;
  width: 300px;
}
.tabs {
  padding-top: 10px;
}
</style>
