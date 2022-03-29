<template>
  <div class="app-container">

<el-form :model="form" label-position="left" class="form" inline>
      <!-- <el-row>
        <el-col :span="6"> -->
      <el-form-item label="矿机名/机器码:">
        <el-input v-model="form.machineId" placeholder="请输入矿机名或机器码" />
      </el-form-item>
      <!-- </el-col>
        <el-col :span="6"> -->
      <el-form-item label="矿机状态:">
        <el-select v-model="form.status" placeholder="请选择状态">
          <el-option label="全部" value="-1" />
          <el-option v-for="item in status" :key="item.value" :label="item.label" :value="item.value" />
        </el-select>
      </el-form-item>
      <!-- </el-col>
        <el-col :span="6"> -->
      <el-form-item label="过期状态:">
        <el-select v-model="form.expired" placeholder="请选择状态">
          <el-option label="全部" value="-1" />
          <el-option v-for="item in expired" :key="item.value" :label="item.label" :value="item.value" />
        </el-select>
      </el-form-item>
      <!-- </el-col>
        <el-col :span="6"> -->
      <el-form-item label="用户名:">
        <el-input v-model="form.userName" placeholder="请输入用户名" />
      </el-form-item>
      <el-button type="primary" @click="searchList()">查询</el-button>
      <!-- </el-col>
      </el-row> -->
    </el-form>







    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row
    >
      <el-table-column align="center" label="性别" >
        <template slot-scope="scope">
          {{ scope.$index }}
        </template>
      </el-table-column>
      <el-table-column label="价格">
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="畅易阁链接" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="生命值" width="110" align="center">
        <template slot-scope="scope">
          {{ scope.row.pageviews }}
        </template>
      </el-table-column>
      <el-table-column class-name="status-col" label="穿刺" width="110" align="center">
        <template slot-scope="scope">
          <el-tag :type="scope.row.status | statusFilter">{{ scope.row.status }}</el-tag>
        </template>
      </el-table-column>
      <el-table-column align="center" prop="created_at" label="火攻" width="200">
        <template slot-scope="scope">
          <i class="el-icon-time" />
          <span>{{ scope.row.display_time }}</span>
        </template>
      </el-table-column>

      <el-table-column label="冰攻" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="玄攻" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="毒攻" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="会心" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="命中" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="修炼评分" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="门派" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="宝石评分" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

      <el-table-column label="红利" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>

    </el-table>
  </div>
</template>

<script>
import { getList } from '@/api/table'

const expired = [
  { label: '已过期', value: 1 },
  { label: '未过期', value: 0 }
]
const status = [
  { label: '在线', value: 1 },
  { label: '离线', value: 0 }
]
const workStatus = [
  { label: '绘图中', value: 1 },
  { label: '未开始', value: 0 },
  { label: '已暂停', value: 2 }
]

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      form: {
        machineId: '',
        status: '-1',
        expired: '-1',
        userName: ''
      },
      expired: Object.freeze(expired),
      status: Object.freeze(status),
      list: [],
      total: 0,
      currentPage: 1,
      pageSize: 50,
      currentMachineId: [], // 当前授权的机器id
      currentEdit: {}, // 当前编辑参数的行
      dialogShowParam: false,
      paramDialogCanEdit: false, // 当前是否可编辑
      multipleSelection: null, // 列表多选的项id
      multipleSelectionItems: [],
      showStopDialog: false,
      currentStop: {},
      showPendingDialog: false,
      pendingTxt: '',
      list: null,
      listLoading: true
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.listLoading = true
      getList().then(response => {
        this.list = response.data.items
        this.listLoading = false
      })
    }
  }
}
</script>
