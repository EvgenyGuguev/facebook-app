<template>
    <div>
        <img src="https://www.publicdomainpictures.net/pictures/310000/velka/new-zealand-landscape.jpg"
             alt="user background image"
             ref="userImage"
             class="object-cover w-full"
        >
    </div>
</template>

<script>
    import Dropzone from 'dropzone';

    export default {
        name: "UploadableImage",

        props: [
            'imageWidth',
            'imageHeight',
            'location',
        ],

        data() {
            return {
                dropzone: null,
            }
        },

        mounted() {
            this.dropzone = new Dropzone(this.$refs.userImage, this.settings);
        },

        computed: {
            settings() {
                return {
                    paramName: 'image',
                    url: '/api/user-images',
                    acceptedFiles: 'image/*',
                    params: {
                        'width': this.imageWidth,
                        'height': this.imageHeight,
                        'location': this.location,
                    },
                    headers: {
                        'X-CSRF-TOKEN': document.head.querySelector('meta[name=csrf-token]').content,
                    },
                    success: (event, response) => {
                        alert('uploaded!');
                    }
                };
            }
        }
    }
</script>

<style scoped>

</style>
