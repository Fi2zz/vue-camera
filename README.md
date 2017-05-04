# vue-camera
原理：使用了input標簽，type=file 和 capture="camera" 屬性

<input accept="image/*" capture="camera" type="file">

@params label     按鈕文字
@params preview   開啓預覽 默認為false

@params v-model   一個FileList對象

@method change   拍照完畢后點擊使用照片后調用  
