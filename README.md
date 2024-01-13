# xqeditor

This is a simplify markdown editor.

[View Chinese documents](./zh.md)

## Install

+ import cdn package

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
<link rel="stylesheet" href="https://xqgj.cc/xqcdn/libs/xqeditor/css/xqeditor.min.css">
<!-- Browser -->
<script src="https://xqgj.cc/xqcdn/libs/xqeditor/js/xqeditor.min.js"></script>
<!-- es module -->
<script type="module">
    import xqgjs from '../lib/js/xqeditor-esm.min.js';
</script>
```

+ Vue

```sh
npm i xqeditor
```

## Usage

### Browser

+ html

```html
<div id="myEditor"></div>
<div class="myeditor-btns">
    <button id="myeditor-btn-set">Set</button>
    <button id="myeditor-btn-get">Get</button>
    <button id="myeditor-btn-img">Img</button>
</div>
```

+ js

```js
// init editor
let myEditor = new XqEditor({
    el: '#myEditor',
});

// setting
let setBtn = document.getElementById('myeditor-btn-set');
let getBtn = document.getElementById('myeditor-btn-get');
let imgBtn = document.getElementById('myeditor-btn-img');
let url = '';

console.log(myEditor);

// set value
setBtn.addEventListener('click', setVal, false);
function setVal () {  
    let val = '# hello \n\n';
    myEditor.setVal(val);
}

// get value
getBtn.addEventListener('click', getVal, false);
function getVal () {
    let result = myEditor.getVal();
    alert('result is '+JSON.stringify(result));
}

// get image
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

+ import

```js
import xqeditor from 'xqeditor';
Vue.use(xqeditor);
```

+ component

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
                content: '', // editor content
                uploadUrl: '', // upload file addr
            }
        }
    },
    methods: {
        // upload image
        uploadImg (files) {
            // your upload method
            // ...

            // upload success
            let url = 'https://xxx.xxx/xxx.jpg';
            this.editor.uploadUrl = url;
        },
        // set Value
        setVal () {
            this.$refs.xqeditor.setVal('# hello');
        },
        // get value
        getVal () {
            this.$refs.xqeditor.getVal();
            // { text: '# hello \n\n ...', html: '<h1>hello</h1>...' }
        },
    }
}
```

## View xqeditor

Run this script to view the demonstration case: `npm run test:browser`.

[【Demo Preview】](https://xqgj.cc/xqeditor/test/browser.html)

![Preview Image](https://xqgj.cc/xqeditor/test/img/preview.jpg)

## ask questions

[submit your question](https://github.com/gitguanqi/xqeditor/issues/new)

## Author

[@gitguanqi](https://github.com/gitguanqi)
