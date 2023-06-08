<template>
    <main class="page-wrapper about-page" v-if="page.length">
        <div class="about-page__image">
            <img :src="page[0].acf.image.url" :alt="page[0].acf.image.alt" />
        </div>
        <TitleAndText v-for="(item, index) in page[0].acf.title_and_text" :key="index" :title="item.title" :text="item.text" />
    </main>
</template>

<script>
import { getData } from '@/utilities/getData.js';
import { endPoint } from '@/constants/endpoint.js';
import TitleAndText from '@/components/TitleAndText';

export default {
    name: 'Contact',
    components: {
        TitleAndText,
    },
    data: () => ({
        page: [],
    }),
    async created() {
        this.page = await getData(`${endPoint}/pages?slug=info`);
    },
    metaInfo() {
        return {
            title: 'Chew Productions - Who we are',
        };
    },
};
</script>
<style lang="scss">
.about-page {
    &__title {
        font-family: $font-family-title;
        text-align: center;
        margin-bottom: 40px;
    }

    &__image {
        max-width: 400px;
        margin: 0 auto 50px auto;
    }
}
</style>
