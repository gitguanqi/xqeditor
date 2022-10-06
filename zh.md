# xqeditor

这是一个简单的markdown文本编辑器。

[查看英文文档](./README.md)

## 安装

+ 导入CDN

```html
<!-- index.html -->
<!-- css -->
<link href="https://cdn.bootcdn.net/ajax/libs/font-awesome/6.2.0/css/all.min.css" rel="stylesheet">
<link href="https://cdn.bootcdn.net/ajax/libs/github-markdown-css/5.1.0/github-markdown.min.css" rel="stylesheet">
<link href="https://cdn.bootcdn.net/ajax/libs/highlight.js/11.6.0/styles/default.min.css" rel="stylesheet">
<!-- js -->
<script src="https://cdn.bootcdn.net/ajax/libs/markdown-it/13.0.1/markdown-it.min.js"></script>
<script src="https://cdn.bootcdn.net/ajax/libs/highlight.js/11.6.0/highlight.min.js"></script>
```

+ Browser

```html
<!-- CSS -->
<link rel="stylesheet" href="https://unpkg.com/xqeditor/lib/css/xqeditor.min.css">
<!-- Browser -->
<script src="https://unpkg.com/xqeditor/lib/js/xqeditor.min.js"></script>
<!-- es module -->
<script type="module">
    import xqgjs from '../lib/js/xqeditor-esm.min.js';
</script>
```

+ Vue

```sh
npm i xqeditor
```

## 使用

### 游览器

+ html

```html
<div id="myEditor"></div>
<div class="myeditor-btns">
    <button id="myeditor-btn-set">设置值</button>
    <button id="myeditor-btn-get">获取值</button>
    <button id="myeditor-btn-img">获取图片</button>
</div>
```

+ js

```js
// 初始化编辑器
let myEditor = new XqEditor({
    el: '#myEditor',
});

// 操作
let setBtn = document.getElementById('myeditor-btn-set');
let getBtn = document.getElementById('myeditor-btn-get');
let imgBtn = document.getElementById('myeditor-btn-img');
let url = '';

console.log(myEditor);

// 设置值
setBtn.addEventListener('click', setVal, false);
function setVal () {  
    let val = '# hello \n\n';
    myEditor.setVal(val);
}

// 获取值
getBtn.addEventListener('click', getVal, false);
function getVal () {
    let result = myEditor.getVal();
    alert('result is '+JSON.stringify(result));
}

// 获取图片
imgBtn.addEventListener('click', getImg, false);
function getImg () {
    let result = myEditor.editor.files;
    if (!result) {
        alert('请先上传图片！');
        return;
    }
    if (url) { 
        URL.revokeObjectURL(url);
    } else {
        url = URL.createObjectURL(result[0]);
    }
    myEditor.addEditor('image', url);
    alert('result is '+JSON.stringify(result));
}
```

### Vue

+ 导入依赖包

```js
import xqeditor from 'xqeditor';
Vue.use(xqeditor);
```

+ 组件中

```html
<xq-editor
    ref="xqeditor"
    :content="editor.content" 
    :url="editor.uploadUrl" 
    @uploadImg="uploadImg"
>
</xq-editor>
<button @click="setVal">Set Value</button>
<button @click="getVal">get Value</button>
```

```js
export default {
    name: 'demo',
    data () {
        return {
            editor: {
                content: '', // 编辑内容
                uploadUrl: '', // 上传图片地址
            }
        }
    },
    methods: {
        // 上传图片
        uploadImg (files) {
            // 你的上传方法
            // ...

            // 上传成功
            let url = 'https://xxx.xxx/xxx.jpg';
            this.editor.uploadUrl = url;
        },
        // 设置编辑内容
        setVal () {
            this.$refs.xqeditor.setVal('# hello');
        },
        // 获取编辑内容
        getVal () {
            this.$refs.xqeditor.getVal();
            // { text: '# hello \n\n ...', html: '<h1>hello</h1>...' }
        },
    }
}
```

## 查看示例

运行这个脚本查看展示案例：`npm run test:browser`。

[【在线预览】](https://unpkg.com/xqeditor/test/browser.html)

![预览图片](https://unpkg.com/xqeditor/test/img/preview.jpg)

## 提问题

[提出问题](https://github.com/gitguanqi/xqeditor/issues/new)

## 作者

[@gitguanqi](https://github.com/gitguanqi)
