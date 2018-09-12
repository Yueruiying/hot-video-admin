<template>
  <div class="app-container">
    <!-- 标题栏 -->
    <el-row>
      <h3>资源列表</h3>
    </el-row>
    <!-- 搜索栏 -->
    <el-row class="search-container">
      <el-form :inline="true">
        <el-col :span="24">
          <el-form-item label="来源桶：">
            <el-select v-model="form.region" placeholder="请选择" clearable style="width:115px">
              <el-option label="区域二1" value="shanghai">
                <span style="float: left; font-size: 13px">1111</span>
              </el-option>
              <el-option label="区域二" value="shanghai1">
                <span style="float: left; font-size: 13px">1111</span>
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Key前缀：">
            <el-select v-model="form.region" clearable style="width:145px">
              <el-option label="区域二1" value="shanghai2">
                <span style="float: left; font-size: 13px">1111111</span>
              </el-option>
              <el-option label="区域四" value="shanghai3">
                <span style="float: left; font-size: 13px">1111111</span>
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSubmit">获取资源</el-button>
          </el-form-item>
        </el-col>
      </el-form>
    </el-row>
    <!-- 表格栏 -->
    <el-row>
      <el-table ref="multipleTable" :data="tableData3" tooltip-effect="dark" style="width: 80%; margin:6px 20px;" @selection-change="handleSelectionChange">
        <el-table-column type="selection" width="55" />
        <el-table-column prop="key" label="Key" width="180" />
        <el-table-column label="Key" width="100">
          <template slot-scope="scope">{{ scope.row.date }}</template>
        </el-table-column>
        <el-table-column prop="capacity" label="大小" width="120" />
        <el-table-column prop="fileType" label="文件类型" show-overflow-tooltip />
      </el-table>
    </el-row>
    <!-- 弹框栏 -->
    <el-row>
      <el-button type="success" @click="onAdd">创建批处理</el-button>
    </el-row>
    <!--dialog弹窗-->
    <el-dialog id="form" :title="dialogTitle" :close-on-click-modal="false" :visible.sync="orderDetail" width="450px">
      <el-form ref="orderForm" :model="order" label-width="100px">
        <el-row>
          <el-col :span="24">
            <el-form-item label="目标通：" prop="ewbNo" style="width: 400px; margin: 15px auto;">
              <el-select v-model="form.region" placeholder="请选择" clearable>
                <el-option label="区域二1" value="shanghai">
                  <span style="float: left; font-size: 13px">1111</span>
                </el-option>
                <el-option label="区域二" value="shanghai1">
                  <span style="float: left; font-size: 13px">1111</span>
                </el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item label="Key模板：" prop="diffPiece" style="width: 400px; margin: 15px auto">
              <el-input v-model="order.diffPiece" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="24">
            <el-form-item label="批处理模板：" prop="handleSuggestion">
              <a href="http://www.baidu.com"><span>1:3分辨率/3带宽/3码率</span></a>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <div slot="footer">
        <el-button :loading="editLoading" type="primary" @click="submitForm('orderForm')">提交</el-button>
        <el-button @click.native="orderDetail = false">取消</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogTitle: '', // dialog弹窗
      orderDetail: false, // 详情
      editLoading: false, // 加载
      order: { // 订单
        ewbNo: '',
        diffPiece: '',
        damagePiece: '',
        handleSuggestion: ''
      },
      form: {
        region: ''
      },
      tableData3: [{
        date: '2016-05-03',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }, {
        date: '2016-05-02',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }, {
        date: '2016-05-04',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }, {
        date: '2016-05-01',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }, {
        date: '2016-05-08',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }, {
        date: '2016-05-06',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }, {
        date: '2016-05-07',
        key: '20180809/一出好戏.mp4',
        capacity: '800M',
        fileType: 'video/mp4'
      }],
      multipleSelection: []
    }
  },
  mounted() {
  },
  methods: {
    onSubmit() {
      console.log('submit!')
    },
    submitForm() {
      console.log('submit!')
    },
    createBatch() {
      this.$prompt('请输入邮箱', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        inputPattern: /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/,
        inputErrorMessage: '邮箱格式不正确'
      }).then(({ value }) => {
        this.$message({
          type: 'success',
          message: '你的邮箱是: ' + value
        })
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '取消输入'
        })
      })
    },
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    onAdd() {
      this.dialogClose('orderForm')
      this.isAdd = true
      this.orderDetail = true
      this.disabled_edit = false
      setTimeout(() => {
        this.resetForm('orderForm')
      }, 200)
      this.dialogTitle = '新增'
      this.$nextTick(() => { // 娓呯┖琛ㄥ崟楠岃瘉
        this.$refs['orderForm'].clearValidate()
      })
    },
    dialogClose(formName) {
      this.resetForm(formName)
      this.orderDetail = false
    },
    // 重置
    resetForm(formName) {
      // this.$refs[formName].resetFields()
      this.order = {
        ewbNo: '',
        diffPiece: '',
        damagePiece: '',
        handleSuggestion: ''
      }
      if (!this.isAdd) {
        this.order.appointNo = this.appointNo_value
      }
    }
  }
}
</script>
<style>
  .search-container {
    margin: 10px;
  }
</style>

