<template>
  <div class="app-container">
    <a-card>
      <!-- 搜索条件部分 - Begin -->
      <a-row>
        <a-input-search
          v-model="query.name"
          placeholder="请输入名称查询"
          style="width: 200px"
          @search="fetchData(pageConf)"
        />
        <a-popover content="刷新">
          <a-button type="dashed" icon="redo" @click="fetchData(pageConf)" />
        </a-popover>
      </a-row>
      <!-- 搜索条件部分 - End -->

      <!-- Table表列表部分 - Begin -->
      <a-table
        size="small"
        :columns="columns"
        :row-key="record => record.id"
        :pagination="false"
        :loading="loading"
        :data-source="list"
        :scroll="{ x: 'calc(700px + 50%)'}"
        bordered
      >
        <span slot="action" slot-scope="text, record">
          <a-popover content="删除">
            <a-button type="dashed" size="small" @click="handleDel(record.id)">
              <a-icon type="delete" theme="twoTone" two-tone-color="#f5222d" />
            </a-button>
          </a-popover>
        </span>
      </a-table>
      <pagination
        v-show="pageConf.total>0"
        :total="pageConf.total"
        :page.sync="pageConf.page"
        :limit.sync="pageConf.limit"
        @pagination="fetchData"
      />
      <!-- Table列表部分 - End -->
    </a-card>
  </div>
</template>

<script>
import Pagination from '@/components/Pagination'
import { delLog, logList } from '@/api/modules/setting/log'

export default {
  name: 'Index',
  components: { Pagination },
  data() {
    return {
      list: [],
      columns: [
        { title: '操作用户', dataIndex: 'username', key: 'username', width: 110 },
        { title: '操作描述', dataIndex: 'operation', key: 'operation' },
        { title: '耗时(毫秒)', dataIndex: 'time', key: 'time', align: 'center', width: 100 },
        { title: 'IP地址', dataIndex: 'ip', key: 'ip', align: 'center', width: 120 },
        { title: '操作时间', dataIndex: 'createTime', key: 'createTime', align: 'center', width: 150 },
        { title: '操作', key: 'action', scopedSlots: { customRender: 'action' }, fixed: 'right', align: 'center', width: 100 }
      ],
      query: {},
      pageConf: {
        page: 1,
        limit: 5,
        total: 0
      },
      loading: true
    }
  },
  created() {
    this.fetchData(this.pageConf)
  },
  methods: {
    fetchData(page) {
      this.loading = true
      this.pageConf.page = page.page
      this.pageConf.limit = page.limit
      logList(this.pageConf, this.query).then(res => {
        this.list = res.data.rows
        this.pageConf.total = res.data.total
        this.loading = false
      })
    },
    handleDel(id) {
      const _this = this
      this.$confirm({
        title: '您确定要删除此条数据吗?',
        okText: '确定',
        okType: 'danger',
        cancelText: '取消',
        onOk() {
          delLog(id).then(res => {
            if (res.code === 200) {
              _this.$message
                .success(res.msg)
            } else {
              _this.$message
                .error(res.msg)
            }
            _this.fetchData(_this.pageConf)
          })
        }
      })
    }
  }
}
</script>

<style scoped>
.ant-row {
  margin-bottom: 10px;
}
</style>
