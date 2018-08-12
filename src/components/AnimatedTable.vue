<template>
    <div class="an-results-table an-animated-results-table">
        <table>
            <thead>
            <tr>
                <th>Candidatura</th>
                <th>Escaños</th>
                <th>Votos</th>
            </tr>
            </thead>
            <tbody name="table-row" is="transition-group">
            <tr v-for="(candidatura,i) in candidaturasWithEscanos"
                class="table-row-item"
                :class="{'an-odd-row': i % 2}"
                :key="i">
                <td class="an-candidatura">{{candidatura.sCandidatura}}</td>
                <td class="an-escanos">{{candidatura.iEscanos}}</td>
                <td class="an-votos">{{candidatura.iVotos|formatNumber}}</td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        props: {
            candidaturas: Array,
        },
        computed: {
            candidaturasWithEscanos() {
                return this.candidaturas && this.candidaturas.filter(c => c.iEscanos !== 0);
            },
        },
        filters: {
            formatNumber(n) {
                return Number(n).toLocaleString();
            },
        },
    };
</script>

<style lang="less" rel="stylesheet/less">
    .an-animated-results-table {
        .table-row-move {
            transition: all .5s;
        }
        .table-row-item {
            backface-visibility: hidden;
            transition: all 1s;
        }
        .table-row-enter, .table-row-leave-to
            /* .list-complete-leave-active below version 2.1.8 */ {
            opacity: 0;
            /*transform: translateY(30px);*/
        }
        .table-row-leave-active {
            position: absolute;
        }
    }
</style>
