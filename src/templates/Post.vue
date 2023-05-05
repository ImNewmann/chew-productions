<template>
    <transition name="fade" appear>
        <VideoPlayer v-if="showModal" :post="post" />
    </transition>
</template>

<script>
import { formatTitle } from '@/utilities/formatTitle.js';
import VideoPlayer from '@/components/VideoPlayer';

export default {
    name: 'Post',

    props: {
        posts: { type: Array, required: true },
    },
    components: {
        VideoPlayer,
    },
    data: () => ({
        title: null,
        videoLength: null,
        showModal: false,
        post: {},
    }),

    metaInfo() {
        const currentRoute = this.$router.currentRoute.params.postSlug;
        return {
            title: 'Chew Productions',
            titleTemplate: `%s - ${formatTitle(currentRoute)}`,
        };
    },
    watch: {
        $route: {
            immediate: true,
            handler: function(newVal) {
                if (newVal.meta && newVal.meta.showModal) {
                    this.showModal = newVal.meta && newVal.meta.showModal;
                    this.getPost();
                }
            },
        },
    },

    methods: {
        getPost() {
            const currentRoute = this.$router.currentRoute.params.postSlug;
            this.title = formatTitle(currentRoute);
            this.post = this.posts.filter((post) => post.slug === currentRoute)[0];
            this.videoLength = this.post.acf.videos.length;
        },
    },
};
</script>
<style lang="scss">
.fade-enter-active,
.fade-leave-active {
    opacity: 0;
}
</style>
