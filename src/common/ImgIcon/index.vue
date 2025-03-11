<template>
    <div class="img-icon" :style="{ width: size + 'px', height: size + 'px' }">
        <img :src="imgSrc" alt="img" class="img-icon-img" />
    </div>
</template>

<script>
    export default {
        name: 'ImgIcon',
        props: {
            imgSrc: {
                type: String,
                required: true
            },
            size: {
                type: Number,
                required: true
            }
        }
    }
</script>

<style lang="scss" scoped>
.img-icon-img{
    width: 100%;

}
.img-icon{
    cursor: pointer;
}
</style>