<template>
    <svg class="an-hemiciclo-chart" :width="width" :height="height" :viewBox="[0,0,width,height].join(' ')">
        <g v-if="sectors" class="an-pie" :transform="`translate(${width/2}, ${height})`">
            <path
                    class="an-sector"
                    :class="`fill-${sector.data.sCandidaturaUnificada}`"
                    v-for="sector in sectors"
                    :d='arc(sector)'/>
        </g>
    </svg>
</template>

<script>
    import * as d3 from 'd3';

    export default {
        name: 'hemiciclo-chart',
        props: {
            currentData: Object,
            previousData: Object,
            showCurrent: Boolean,
        },
        data() {
            return {
                width: 400,
                height: 200,
            };
        },
        computed: {
            candidaturas() {
                return this.showCurrent
                    ? this.currentData && this.currentData.candidaturas
                    : this.previousData && this.previousData.candidaturas;
            },
            candidaturasWithEscanos() {
                return this.candidaturas && this.candidaturas.filter(c => c.iEscanos !== 0);
            },
            sectors() {
                return this.candidaturasWithEscanos && this.pie(this.candidaturasWithEscanos);
            },
            arc() {
                return d3.arc()
                    .innerRadius(50)
                    .outerRadius(200);
            },
            pie() {
                const options = {
                    additionalAngle: -Math.PI * 0.04,
                };
                return d3.pie()
                    .startAngle(-Math.PI / 2 - options.additionalAngle)
                    .endAngle(Math.PI / 2 + options.additionalAngle)
                    .padAngle(Math.PI / 180.0 * 0.2)
                    .value(d => d.iEscanos)
                    .sort(null);
            },
        },
    };
</script>

<style lang="less">

    @pp           : #11a3de;
    @psoe         : #d20a11;
    @ciudadanos   : #ec6b27;
    @podemos      : #6e2362;

    @iu           : #009f62;
    @pnv          : #006634;
    @upyd         : #e7548e;
    @ciu          : #2E3272; // CDC - // Democracia i Llibertat -

    @amaiur       : #118f9f;
    @bildu        : #b3c900;
    @ccanaria     : #eeda00;
    @bng          : #8dd8f8;

    @gbai         : #ae2f17;
    @esquerra     : #fe9f08;
    @compromis    : #ec4f07;
    @fac          : #17375e;

    @otros        : #93a2a9;
    @sinasignar   : rgb(204, 204, 204);


    .an-hemiciclo-chart {
        .an-sector {
            fill: gray;

            &.fill-sinasignar   { fill: @sinasignar;   }
            &.fill-otros        { fill: @otros;        }
            &.fill-pp           { fill: @pp;           }
            &.fill-psoe         { fill: @psoe;         }
            &.fill-ciudadanos   { fill: @ciudadanos;   }
            &.fill-podemos      { fill: @podemos;      }
            &.fill-podemos-iu   { fill: @podemos;      }
            &.fill-iu           { fill: @iu;           }
            &.fill-pnv          { fill: @pnv;          }
            &.fill-upyd         { fill: @upyd;         }
            &.fill-ciu          { fill: @ciu;          }
            &.fill-amaiur       { fill: @amaiur;       }
            &.fill-bildu        { fill: @bildu;        }
            &.fill-ccanaria     { fill: @ccanaria;     }
            &.fill-bng          { fill: @bng;          }
            &.fill-gbai         { fill: @gbai;         }
            &.fill-esquerra     { fill: @esquerra;     }
            &.fill-compromis    { fill: @compromis;    }
            &.fill-fac          { fill: @fac;          }
        }
    }
</style>
