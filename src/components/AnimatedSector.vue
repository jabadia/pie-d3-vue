<template>
    <path
            class="an-sector"
            :class="`fill-${sector.data.sCandidaturaUnificada}`"
            :d='arc(animatedSector)'/>
</template>

<script>
    import * as d3 from 'd3';
    import TweenLite from 'gsap';

    export default {
        props: {
            sector: Object,
        },
        data() {
            return {
                animatedSector: {
                    startAngle: 0,
                    endAngle: 0,
                    padAngle: 0,
                },
            };
        },
        watch: {
            sector: {
                immediate: true,
                handler(newSector) {
                    // console.log(newSector.data.sCandidaturaUnificada, newSector.startAngle, newSector.endAngle);
                    TweenLite.to(this.animatedSector, 0.5, {
                        startAngle: newSector.startAngle,
                        endAngle: newSector.endAngle,
                        padAngle: newSector.padAngle,
                    });
                },
            },
        },
        computed: {
            arc() {
                return d3.arc()
                    .innerRadius(50)
                    .outerRadius(200);
            },
        },
    };
</script>

<style lang="less" rel="stylesheet/less">
</style>
