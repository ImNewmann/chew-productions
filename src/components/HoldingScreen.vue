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
        <div class="holding-screen__text">
            <p>Film production based in London.</p>
            <button class="holding-screen__cta" @click="handleEnterSiteClicked">Enter site</button>
        </div>

        <!-- <vimeo-player
            class="holding-screen__video"
            ref="player"
            :options="options"
            video-url="https://vimeo.com/833677581/180b6a8f94"
            :controls="false"
            autoplay
            loop
            @play="this.videoReady"
        ></vimeo-player> -->
    </div>
</template>

<script>
export default {
    data() {
        return {
            loaded: false,
            options: {
                muted: true,
            },
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

    [data-ready='true'] ~ &__text {
        opacity: 1;
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
        display: block;
        cursor: pointer;
        font-family: $font-family-content;
        font-size: 20px;
        letter-spacing: 2px;
        text-transform: uppercase;
        position: absolute;
        top: 75%;
        left: 50%;
        transform: translate(-50%, -50%);
        border: 1px $white solid;
        padding: 10px 20px;
        color: $white;
        background: transparent;

        @include breakpoint(desktop) {
            transition: opacity 0.6s ease;
            opacity: 0.8;

            &:hover {
                opacity: 1;
            }
        }
    }
}

.holding-leave-active {
    opacity: 0;
    transition: all 0.3s ease;
}
</style>
