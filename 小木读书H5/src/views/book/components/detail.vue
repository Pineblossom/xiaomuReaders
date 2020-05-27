<template>
  <el-form>
    <sticky :class-name="'sub-navbar'">
      <el-button @click="showGuild">显示帮助</el-button>
      <el-button
        :loading="loading"
        type="success"
        @click="submitBook"
      >{{ isEdit ? '编辑电子书' : '新增电子书' }}</el-button>
    </sticky>
    <div class="detail-container">
      <Warning />
      <el-row>
        <el-col :sapn="24">
          <!-- 表单控件的具体样式 -->
          <ebook-upload />
        </el-col>
        <el-col :sapn="24" />
      </el-row>
    </div>
  </el-form>
</template>

<script>
import Warning from './warning'
import Sticky from '../../../components/Sticky/index'
import EbookUpload from '../../../components/EbookUpload/index'
export default {
  components: {
    Sticky,
    Warning,
    EbookUpload
  },
  props: {
    isEdit: Boolean
  },
  data() {
    return {
      loading: false
    }
  },
  methods: {
    showGuild() {
      console.log('this is guild...')
    },
    submitBook() {
      this.loading = true
      setTimeout(() => {
        this.loading = false
      }, 1000)
    }
  }
}
</script>

<style lang="scss" scoped>
.detail-container {
  padding: 40px 50px 20px;
}
</style>
