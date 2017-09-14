<template>
    <div class="vue-camera">
        <div class="camera-hidden">
            {{label}}
            <input accept="image/*" capture="camera" type="file" @change="change">
        </div>
        <div v-show="preview" class="camera-preview" ref="preview"></div>
    </div>
</template>
<style lang="scss" src="./style.scss" scoped></style>
<script>
    module.exports = {
        props: {
            label: {
                type: String,
                default: 'TAKE PHOTO'
            },
            preview: Boolean
        },
        data() {
            return {
                picture: {}
            }
        },

        watch: {
            picture: {
                deep: true,
                handler(picture) {
                    this.$emit('input', picture);
                    this.$emit('change')
                    this.preview(picture)
                }
            }
        },
        methods: {
            change(e) {
                const picture = e.target.files || e.dataTransfer.files;
                if (!picture.length) {
                    return
                }

                this.picture = picture
            },
            preview(picture) {
                const reader = new FileReader();
                reader.readAsDataURL(picture[0]);
                reader.addEventListener('load', () => {
                    this.createPreviewField(reader.result);
                });
            },
            createPreviewField(src) {
                let photo;
                if (!photo) {
                    photo = document.createElement('img');
                    this.$refs['preview'].appendChild(photo);
                }
                photo.src = src
            }
        }
    }
</script>
