# 文件上传组件

## 当前可配置功能
- 常规文件上传
- 预览上传成功文件的大小
- 限制上传文件大小
- 限制上传文件数量
- 限制上传文件格式
- 上传头像
- 上传图片显示成功列表
- 卡片式文件列表
- 拖拽上传
- 点击预览功能

---
## Build Setup

```html
//在当前vue文件中引入依赖文件
import Swiper from '../common/upload'

//html中的实例 propOption为配置项对象
    <upload :propOption='options.normalUpload'></upload>
```
#### 默认配置示例
``` javascript
    // 其中propClass和action为必填属性，本示例中的值均为不设置时的默认值
    propOption: {
        propId: '', //组件容器的id名，后续作为唯一标识 必填
        action: '', //上传的地址
        accept: '', //默认的上传文件格式，多类型时用逗号隔开 描述方式有两种
                    //1.audio/*,video/*,image/* 例image/jpg、audio/mp3
                    //2.后缀名 .png,.jpg
        fileList: [], //文件列表的接收数组
        limit: 3, //最大上传文件数量
        maxSize: 10, //最大上传文件的大小，单位为MB
        multiple: false, //是否支持多个文件一起上传
        buttonText: '', //选择文件按钮的文字内容
        submitText: '', //上传按钮的文字内容
        showFileList: true, //是否显示上传文件的列表
        listType: 'text', //文件列表的形式 text/picture/picture-card
        withCredentials: false, //支持发送 cookie 凭证信息
        autoUpload: false, //是否选择文件后自动上传
        headers: {}, //设置上传的请求头部
        data: {}, //上传时附带的额外参数
        name: 'file', //上传的文件字段名
        handleSuccess: function () {
          this.$message.success('OK')
        } //上传成功时的回调方法
      }
```


# ElementUpload-2nd
