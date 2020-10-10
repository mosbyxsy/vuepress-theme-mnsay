<template>
    <div id="global-layout">
        <DefaultGlobalLayout/><br>
        <!--<Live2D v-if="!isMobile"/>-->
        <Robot />
    </div>
</template>

<script>
    import GlobalLayout from '@app/components/GlobalLayout.vue'
    import Robot from '@theme/components/Robot.vue';
    // import Live2D from '@theme/components/Live2D';
    // import isMobile from 'is-mobile';

    export default {
        name: 'GlobalLayout',
        data () {
            return {
                isMobile : true
            };
        },
        components: {
            DefaultGlobalLayout: GlobalLayout,
            Robot,
            // Live2D
        },
        mounted () {
            // this.isMobile = isMobile();
        }
    }
</script>