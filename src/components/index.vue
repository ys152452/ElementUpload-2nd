<template>
  <div class='example'>
    <h2>常规上传</h2>
    <upload :propOption='options.normalUpload'></upload>
    <br>
    <hr>
    <h2>预览文件大小</h2>
    <upload :propOption='options.listUpload'></upload>
    <br>
    <hr>
    <h2>限制文件大小和数量</h2>
    <upload :propOption='options.exceedUpload'></upload>
    <br>
    <hr>
    <h2>限制文件格式</h2>
    <upload :propOption='options.acceptUpload'></upload>
    <br>
    <hr>
    <h2>上传头像</h2>
    <upload :propOption='options.avatarUpload'></upload>
    <br>
    <hr>
    <h2>上传图片列表</h2>
    <upload :propOption='options.imageListUpload'></upload>
    <br>
    <hr>
    <h2>图片列表</h2>
    <upload :propOption='options.cardListUpload'></upload>
    <br>
    <hr>
    <h2>可拖拽</h2>
    <upload :propOption='options.dragUpload'></upload>
    <br>
    <hr>
    <h2>自动上传</h2>
    <upload :propOption='options.ctrUpload'></upload>
  </div>
</template>

<script>
import upload from '../common/upload'
export default {
  data () {
    return {
      options: {
        normalUpload: {
          propId: 'uploadNormal',
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [
            {
              name: 'food.jpeg',
              url:
                'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'
            },
            {
              name: 'food2.jpeg',
              url:
                'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'
            }
          ],
          multiple: true,
          submitText: 'submit',
          buttonText: 'upload'
        },
        listUpload: {
          propId: 'uploadPreSize',
          multiple: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          buttonText: '选择文件',
          submitText: '点击上传'
        },
        acceptUpload: {
          propId: 'uploadAccept',
          multiple: true,
          accept: '.txt',
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          buttonText: '选择文件',
          submitText: '点击上传'
        },
        exceedUpload: {
          propId: 'uploadExceedSize',
          limit: 3,
          maxSize: 2,
          multiple: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          buttonText: '选择文件',
          submitText: '点击上传'
        },
        avatarUpload: {
          propId: 'uploadAvatar',
          showFileList: false,
          maxSize: 2,
          multiple: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          imgSize: {
            width: '178px',
            height: '178px'
          },
          listType: 'picture-card'
        },
        imageListUpload: {
          propId: 'uploadImageList',
          maxSize: 2,
          multiple: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          imgSize: {
            width: '178px',
            height: '178px'
          },
          listType: 'picture-card'
        },
        cardListUpload: {
          propId: 'uploadCardList',
          maxSize: 2,
          multiple: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          buttonText: '选择文件',
          submitText: '点击上传',
          listType: 'picture'
        },
        dragUpload: {
          propId: 'uploadDrag',
          multiple: true,
          drag: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          buttonText: '选择文件',
          submitText: '点击上传'
        },
        ctrUpload: {
          propId: 'uploadControl',
          multiple: true,
          action: 'https://jsonplaceholder.typicode.com/posts/',
          fileList: [],
          buttonText: '选择文件',
          submitText: '点击上传',
          control: true,
          autoUpload: true
        }
      }
    }
  },
  methods: {
  },
  components: {
    upload: upload
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.example {
  width: 600px;
  margin: 0 auto;
}
</style>
