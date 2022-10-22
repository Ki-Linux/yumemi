<template>
    <div class="PoplulationGraph">
        <top_title/>
        <table_list/>
        <div class="parentChart">
            <chart />
        </div>
    </div>
</template>
<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator';
import TopTitle from '@/components/TopTitle.vue';
import TableList from '@/components/TableList.vue';
import Chart from '@/components/BarChart.vue';
@Component({
    components: {
        'top_title': TopTitle,
        'table_list': TableList,
        Chart,
    }
})
export default class PoplulationGraph extends Vue{
    
}
</script>
<style>
/*phone*/
@media screen and (max-width: 480px) {
    .parentChart {
        padding: 5px;
    }
}
/*タブレット*/
@media screen and (min-width: 481px) and (max-width: 959px) {
    .parentChart {
        padding: 15px;
    }
}
/*pc*/
@media screen and (mix-width: 960px) {
    .parentChart {
        padding: 20px;
    }
}
</style>