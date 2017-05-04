<template>
    <div class="vue-camera">
        <div class="camera-hidden">
            {{label}}
            <input accept="image/*" capture="camera" type="file" @change="change">
        </div>
        <div v-if="preview" class="camera-preview" :id="uuid"></div>
    </div>
</template>
<style lang="scss" src="./style.scss" scoped></style>
<script>
    module.exports = {
        props: {
            label: {
                type: String,
                default: '點擊拍照'
            },
            preview: Boolean
        },
        data(){
            return {
                emitter: {}
            }
        },
        created(){
            this.uuid = 'camera-' + Math.random().toString(36).substring(3, 8)
        },
        methods: {
            change(e){
                const picture = e.target.files || e.dataTransfer.files;
                if (!picture.length) {
                    return
                }
                this.$emit('input',picture)
                if (this.preview) {
                    this.onPreview(picture)
                }
            },
            onPreview(picture){
                const reader = new FileReader();
                reader.readAsDataURL(picture[0]);
                reader.addEventListener('load', ()=> {
                    this.createPreviewField(reader.result);
                });
            },
            createPreviewField(src){
                this.photo = document.createElement('img');
                document.getElementById(this.uuid).appendChild(this.photo);
                this.photo.src = src
            }
        }
    }
</script>
