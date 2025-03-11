<template>
    <div>
        <ChapterHeader :title="title"></ChapterHeader>
        <div class="content" :style="{ marginTop: spacing + 'px' }">
            <slot></slot>
        </div>
    </div>
</template>

<script>
import ChapterHeader from './ChapterHeader.vue';

export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Chapter',
    components: {
        ChapterHeader,
    },
    props: {
        title: {
            type: String,
            required: true,
        },
        spacing: {
            type: Number,
            default: 16,  // 默认间距为 16px
        },
    },
};
</script>

<style lang="scss" scoped>
.content {
    // 间距现在通过 prop 和内联样式控制
}
</style>
