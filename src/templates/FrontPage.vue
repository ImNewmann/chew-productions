<template>
    <section :class="['posts', this.scrollLock ? 'lock-scroll' : '']">
        <VideoCarousel v-if="this.featuredCategory" :posts="getPostsFromCategories(this.featuredCategory.id)" :orientation="this.featuredCategory.acf.orientation" />
        <div v-for="(category, index) in categories" :key="index">
            <VideoCarousel
                v-if="category.slug !== 'featured-work'"
                :posts="getPostsFromCategories(category.id)"
                :orientation="category.acf.orientation"
                :slidesPerViewDesktop="3.1"
                :slidesPerViewMobile="1.2"
            />
        </div>
        <router-view :posts="posts"></router-view>
    </section>
</template>

<script>
import VideoCarousel from '@/components/VideoCarousel';

export default {
    name: 'FrontPage',
    props: {
        posts: { type: Array, required: true },
        categories: { type: Array, required: true },
    },
    components: { VideoCarousel },

    data: () => ({
        scrollLock: false,
        featuredCategory: null,
    }),

    created() {
        this.featuredCategory = this.categories.filter((cat) => cat.slug === 'featured-work')[0];
    },
    methods: {
        getPostsFromCategories(categoryID) {
            return this.posts.filter((post) => post.categories[0] === categoryID);
        },
    },
};
</script>

<style lang="scss">
.posts {
    margin: 0 auto;
    margin-top: 200px;
    width: 90%;
    padding-bottom: 65px;

    // @include breakpoint(desktop) {
    //     max-width: 1400px;
    // }

    .category-title {
        font-family: $font-family-title;
        margin-bottom: 20px;
        color: $white;
    }

    .video-carousel {
        margin-bottom: 40px;
    }
}

.lock-scroll {
    overflow: hidden;
}
</style>
