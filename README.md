# xqeditor

This is a simplify markdown editor.

[View Chinese documents](./zh.md)

## Install

+ Vue

```sh
npm i xqeditor
```

## Usage

+ import

```js
import xqeditor from 'xqeditor';
Vue.use(xqeditor);
```

+ component

```html
<xq-editor 
    :content="editor.content" 
    :url="editor.uploadUrl" 
    @uploadFile="uploadFile"
    @getCurrentValue="getCurrentValue"
>
</xq-editor>
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
        // upload file
        uploadFile (files) {
            // your upload method
            // ...

            // upload success
            let url = 'https://xxx.xxx/xxx.jpg';
            this.editor.uploadUrl = url;
        },
        // get editor value
        getCurrentValue (val) {  
            if (val) {
                this.editor.content = val;
            }
        },
    }
}
```

## View xqeditor

Run this script to view the demonstration case: `npm run test:browser`.

## ask questions

[submit your question](https://github.com/gitguanqi/xqeditor/issues/new)

## Author

[@gitguanqi](https://github.com/gitguanqi)
