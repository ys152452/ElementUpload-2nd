<template>
  <div class="upload-box">
    <el-upload
      :id='option.propId'
      :ref='option.propId'
      :action='option.action'
      :on-preview='handlePreview'
      :multiple='option.multiple'
      :limit='option.limit'
      :drag='option.drag'
      :show-file-list="option.showFileList"
      :auto-upload='option.autoUpload'
      :with-credentials='option.withCredentials'
      :headers='option.headers'
      :accept='option.accept'
      :list-type="option.listType"
      :on-remove='handleRemove'
      :before-remove='beforeRemove'
      :before-upload='beforeUpload'
      :on-exceed='handleExceed'
      :on-change='handleChange'
      :on-success='option.handleSuccess'
      :on-error='handleError'
      :file-list='fileList'>
      <el-button size='small' type='primary' slot="trigger" v-if="(!option.imgSize || option.listType === 'picture') && !option.drag">{{option.buttonText}}</el-button>
      <el-button style="margin-left: 10px;" v-if="(!option.imgSize || option.listType === 'picture') && !option.autoUpload && !option.drag" size="small" type="success" @click="handleSubmit">{{option.submitText}}</el-button>
      <i class="el-icon-upload" v-if="option.drag"></i>
      <div class="el-upload__text" size='small' type='primary' v-if="option.drag">{{dragTip}}<em>{{option.buttonText}}</em></div>
      <i class="el-icon-plus" v-if="imageUrl || option.listType === 'picture-card'"></i>
      <div slot='tip' class='el-upload__tip'>{{option.warningText}}</div>
    </el-upload>
    <el-button style="margin-top: 10px;" v-if="(!option.imgSize || option.listType === 'picture') && !option.autoUpload && option.drag" size="small" type="success" @click="handleSubmit">{{option.submitText}}</el-button>
    <el-dialog :visible.sync="dialogVisible" width="50%">
      <img width="100%" :src='dialogUrl' v-if='isImg'/>
      <iframe  v-if='!isImg' :class="'upload-iframe upload-iframe-' + option.propId" :src="dialogUrl"></iframe>
    </el-dialog>
    <img v-if="imageUrl && option.imgSize" :src="imageUrl" class="el-upload-avatar" :width='option.imgSize.width' :height='option.imgSize.height'>
  </div>
</template>

<script>
export default {
  props: {
    'propOption': {
      type: Object,
      default: {}
    }
  },
  created () {
    this.option = Object.assign(this.optionDefault, this.propOption)
  },
  data () {
    return {
      option: {},
      optionDefault: {
        propId: '',
        action: '',
        accept: '',
        fileList: [],
        limit: 3,
        maxSize: 10,
        multiple: false,
        buttonText: '',
        submitText: '',
        showFileList: true,
        name: 'file',
        listType: 'text',
        withCredentials: false,
        autoUpload: false,
        headers: {},
        data: {},
        handleSuccess: function () {
          this.$message.success('OK')
        }
      },
      isImg: true,
      dialogVisible: false,
      imageUrl: '',
      dialogUrl: '',
      fileList: this.propOption.fileList,
      onChangeItemInfo: {},
      dragTip: `拖拽上传或`,
      typeErrorTip: '格式不正确',
      sizeErrorTip: '上传头像图片大小不能超过',
      overLimitTip: `最多可以选择$overLimitTip$张图片`,
      confirmTip: '确认删除'
    }
  },
  mounted () {
    // const _this = this
    // this.$refs['upload-iframe-' + this.option.propId].addEventListener('open', function () {
    //   _this.previewInDialog()
    // })
  },
  methods: {
    handleSubmit () {
      this.$refs[this.option.propId].submit()
    },
    handleChange (file, fileList) {
      if (file.status === 'success') {
        if (this.option.imgSize && !this.option.showFileList) {
          this.imageUrl = URL.createObjectURL(file.raw)
        }
      }
      fileList.forEach((item, index) => {
        if (item.status === 'success' && !this.imageUrl && !this.dialogUrl) {
          if (document.getElementById(this.propOption.propId).getElementsByClassName('el-upload-list__item-name')[index].innerText === item.name) {
            document.getElementById(this.propOption.propId).getElementsByClassName('el-upload-list__item-name')[index].innerHTML += `&nbsp;&nbsp;&nbsp;&nbsp;${(item.size / 1024).toFixed(2)}KB`
          }
        }
      })
    },
    handlePreview (file) {
      const fileType = file.name.split('.')[file.name.split('.').length - 1].toLowerCase()
      const imgType = ['jpg', 'png', 'jpeg', 'gif', 'img']
      this.isImg = imgType.indexOf(fileType) !== -1
      this.dialogUrl = file.url
      this.dialogVisible = true
    },
    beforeUpload (file) {
      if (this.propOption.maxSize && file.size / 1024 / 1024 > this.propOption.maxSize) {
        this.$message.error(`${this.sizeErrorTip}${this.propOption.maxSize}MB`)
        return false
      }
      if (file.type !== this.option.accept && this.propOption.accept && this.option.accept.indexOf(file.name.split('.')[file.name.split('.').length - 1].toLowerCase()) === -1) {
        this.$message.error(`${this.typeErrorTip}`)
        return false
      }
    },
    handleExceed (file, fileList) {
      const isNotOver = fileList.length < this.option.limit
      if (isNotOver) {
        this.$message.error(this.overLimitTip.replace('$overLimitTip$', this.option.limit))
      }
      return isNotOver
    },
    handleSuccess () {
      this.option.handleSuccess()
    },
    handleError () {
      this.$message.error('上传失败')
    },
    handleRemove (file, fileList) {
      // console.log(file)
      // console.log(fileList)
    },
    beforeRemove (file, fileList) {
      if (file.status === 'success') {
        return this.$confirm(`${this.confirmTip}${file.name}？`)
      }
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style>
.el-upload-list__item-name{
  text-align: left;
}
.el-upload-list{
  box-sizing: border-box;
  padding: 0 12%;
}
.el-upload-list .item-size{
  float: right;
}
.el-upload-avatar{
  width: 178px;
  height: 178px;
  margin-top: 20px;
}
.item-size{
  display: block !important;
  font-size: 12px !important;
  float: left;
}
.upload-box iframe {
  border:0;
}
</style>
