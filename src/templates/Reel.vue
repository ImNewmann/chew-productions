<template>
    <div class="reel">
        <vimeo-player class="reel__video" ref="player" video-url="https://vimeo.com/833677581/180b6a8f94" controls></vimeo-player>
    </div>
</template>

<script>
export default {
    metaInfo() {
        return {
            title: 'Chew Productions - Reel',
        };
    },
};
</script>

<style lang="scss">
.reel {
    display: flex;
    min-height: 100vh;
    margin-top: 200px;

    &__video {
        width: 100vw;
        height: 75vh;
        iframe {
            height: 100%;
            width: 100%;
        }
    }
}
</style>
