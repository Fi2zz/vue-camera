# vue-camera
原理：使用`input`的`type=file` & `capture="camera"` 属性

|prop | type | description|
|----  	|----   	|----		  	      |
|label		|String	| 点击拍照按钮文字    |
|preview  |Boolean  | 开启预览，默认false |
|change   |Event    | 拍照完毕后调用	   |

`v-model`返回一个`FileList`对象

在部分安卓机上可能会弹出对话框选择使用`相册`还是`拍照`，选`拍照`即可





