<template>
    <div id="app">
        <transition name="holding">
            <HoldingScreen v-if="showHolding" @enter-site="handleEnterSite" />
        </transition>
        <transition name="nav" appear>
            <Navbar v-if="!showHolding" :posts="posts" :categories="categories" />
        </transition>
        <transition name="page" appear>
            <router-view v-if="!showHolding" :posts="posts" :categories="categories"></router-view>
        </transition>
        <transition name="footer" appear>
            <Footer v-if="!showHolding" />
        </transition>
    </div>
</template>

<script>
import { endPoint } from '@/constants/endpoint.js';
import { getData } from '@/utilities/getData.js';
import { preloadImages } from '@/utilities/preloadImages.js';
import HoldingScreen from '@/components/HoldingScreen2';
import Navbar from '@/components/Navigation/Navbar';
import Footer from '@/components/Footer';
import '@/assets/scss/main.scss';

export default {
    name: 'App',
    components: {
        HoldingScreen,
        Navbar,
        Footer,
    },

    data: () => ({
        postsLoaded: false,
        showHolding: false,
        posts: [],
        categories: [],
    }),

    metaInfo: {
        // if no subcomponents specify a metaInfo.title, this title will be used
        title: 'Chew Productions',
        // all titles will be injected into this template
        // titleTemplate: '%s | Chew Productions',
    },

    async created() {
        this.showHolding = this.$route.name === 'FrontPage';

        const categories = await getData(`${endPoint}/categories?orderby=id`);
        this.categories = categories.filter((category) => category.slug !== 'uncategorised');

        this.posts = await getData(`${endPoint}/posts?per_page=100`);

        const featuredCategory = this.categories.filter((cat) => cat.id === 8)[0];
        const imagesToLoad = this.getProjectImages(featuredCategory);

        Promise.all(imagesToLoad.map(preloadImages)).then(() => {
            setTimeout(() => {
                this.postsLoaded = true;
            }, 500);
        });
    },

    watch: {
        $route() {
            this.showHolding = false;
        },
    },

    methods: {
        getProjectImages(featuredCat) {
            let visibleImages = [];

            const featuredPosts = this.posts.filter((post) => post.categories.includes(featuredCat.id));

            // 4 Visible projects on screen
            for (let i = 0; i <= 3; i++) {
                visibleImages.push(featuredPosts[i].acf.featured_image.url);
            }
            return visibleImages;
        },

        handleEnterSite() {
            this.showHolding = false;
        },
    },
};
</script>
<style lang="scss" scoped>
.page-enter {
    opacity: 0;
}
.page-enter-to {
    opacity: 1;
    transition: all 0.3s 0.5s ease;
}
.page-leave-active {
    opacity: 0;
    transition: all 0.3s ease;
}
</style>
