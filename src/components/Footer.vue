<template>
    <footer class="footer">
        <div class="footer__links">
            <a href="mailto:hello@chew.productions">hello@chew.productions</a>
            <span>/</span>
        </div>
        <div class="footer__links">
            <SocialLinks />
        </div>
    </footer>
</template>

<script>
import SocialLinks from '@/components/SocialLinks';

export default {
    name: 'Footer',
    components: {
        SocialLinks,
    },
};
</script>

<style lang="scss">
.footer {
    position: absolute;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    width: 100%;
    background-color: $black;
    padding: 20px;
    text-align: center;
    color: $white;

    .page & {
        background-color: $white;
    }

    &__links {
        font-family: $font-family-content;
        color: $white;

        .page & {
            color: $black;
        }

        a {
            transition: opacity 0.3s ease;

            &:hover {
                opacity: 0.7;
            }
        }

        span {
            padding: 0 15px;
        }
    }
}

.footer-enter {
    opacity: 0;
}

.footer-enter-to {
    opacity: 1;
    transition: opacity 0.6s 2s ease;
}
</style>
