<template>
    <div class="holding-screen">
        <iframe
            class="holding-screen__video"
            id="vimeo-video"
            loading="eager"
            preload="auto"
            title="Name"
            src="https://player.vimeo.com/video/833988948?h=f7ee951061&background=1&loop=1&autopause=0&muted=1&quality=auto&responsive=1&dnt=1&app_id=122963"
            width="100%"
            height="100%"
            frameborder="0"
            allow="autoplay; fullscreen"
            allowfullscreen
        ></iframe>

        <div class="holding-screen__content">
            <transition name="logo-holding" appear>
                <Logo />
            </transition>
            <div class="holding-screen__cta">
                <button @click="handleEnterSiteClicked">Enter site</button>
            </div>
        </div>
    </div>
</template>

<script>
import Logo from '@/assets/svg/main-logo.svg';
export default {
    components: {
        Logo,
    },
    data() {
        return {
            loaded: false,
        };
    },
    methods: {
        handleEnterSiteClicked() {
            this.$emit('enter-site');
        },
    },
};
</script>

<style lang="scss">
.holding-screen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;

    iframe {
        width: 100vw;
        height: 56.25vw; /* Given a 16:9 aspect ratio, 9/16*100 = 56.25 */
        min-height: 100vh;
        min-width: 177.77vh; /* Given a 16:9 aspect ratio, 16/9*100 = 177.77 */
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        opacity: 0;
        transition: opacity 0.6s 1s ease;
        z-index: -1;
    }

    [data-ready='true'] {
        opacity: 0.8;
    }

    [data-ready='true'] ~ &__content &__cta {
        opacity: 1;
    }

    &__content {
        display: flex;
        flex-direction: column;
        align-items: center;
        max-width: 300px;
        position: relative;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);

        // @include breakpoint(desktop) {
        //     max-width: 15vw;
        // }

        svg {
            fill: $white;
            path: {
                fill: transparent;
            }
        }
    }

    &__text {
        transition: opacity 0.6s 1s ease;
        opacity: 0;
        p {
            display: block;
            width: 100%;
            font-family: $font-family-content;
            text-align: center;
            position: absolute;
            font-size: 30px;
            line-height: 1.2;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: $white;

            @include breakpoint(desktop) {
                font-size: 40px;
            }
        }
    }

    &__cta {
        position: relative;
        margin-top: 40px;
        opacity: 0;
        transition: opacity 0.6s 1s ease;

        button {
            display: block;
            cursor: pointer;
            font-family: $font-family-content;
            font-size: 20px;
            letter-spacing: 2px;
            text-transform: uppercase;
            border: none;
            padding: 10px 20px;
            color: $white;
            background: transparent;
            transition: opacity 0.6s ease;

            &:after {
                content: '';
                background: $white;
                position: absolute;
                bottom: 0;
                left: 50%;
                transform: translateX(-50%);
                width: 100%;
                height: 2px;
                transition: transform 0.3s ease;
            }

            @include breakpoint(desktop) {
                opacity: 0.8;

                &:after {
                    transform-origin: center;
                    transform: translateX(-50%) scaleX(0.2);
                }

                &:hover {
                    opacity: 1 !important;

                    &:after {
                        transform: translateX(-50%) scaleX(0.8);
                    }
                }
            }
        }
    }
}

.holding-leave-active {
    opacity: 0;
    transition: all 0.3s ease;
}

.logo-holding-enter {
    opacity: 0;
}

.logo-holding-enter-to {
    opacity: 1;
    transition: opacity 1s ease;
}
</style>
