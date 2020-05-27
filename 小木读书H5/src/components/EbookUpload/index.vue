<template>
  <div class="upload-container">
    <el-upload
      :action="action"
      :headers="headers"
      :multiple="false"
      :limit="1"
      :before-upload="beforeUpload"
      :on-success="onSuccess"
      :on-error="onError"
      :on-remove="onRemove"
      :file-list="fileList"
      :on-exceed="onExceed"
      :disabled="disabled"
      drag
      show-file-list
      accept="application/epub+zip"
      class="image-upload"
    >
      <i class="el-icon-upload" />
      <div v-if="fileList.length === 0" class="el-upload__text">
        将文件拖到此处，或<em>点击上传</em>
      </div>
      <div v-else class="el-upload__text">图书已上传</div>
    </el-upload>
  </div>
</template>

<script>
import { getToken } from '../../utils/auth'
export default {
  props: {
    fileList: {
      type: Array,
      default() {
        return []
      }
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      action: `http://localhost:5000/book/upload`
    }
  },
  computed: {
    headers() {
      return {
        Authorization: `Bearer ${getToken()}`
      }
    }
  },
  methods: {
    // 上传文件之前触发
    beforeUpload(file) {
      console.log(file)
      this.$emit('beforeUpload', file)
    },
    // 文件上传成功时的钩子
    onSuccess() {},
    // 文件上传失败时的钩子
    onError(err) {
      console.log({ err })
      const errMsg = err.message && JSON.parse(err.message)
      this.$message({
        message:
          (errMsg && errMsg.msg && `上传失败！失败原因：${errMsg.msg}`) ||
          '上传失败！',
        type: 'error'
      })
      this.$emit('onError', err)
    },
    // 文件列表移除文件时的钩子
    onRemove() {},
    // 文件超出个数限制时的钩子
    onExceed() {}
  }
}
</script>

<style>
</style>
