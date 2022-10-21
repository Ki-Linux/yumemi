<template>
    <div>
        <top_title/>
        <table_list @toGraph="graphShow"/>
    </div>
</template>
<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator';
import TopTitle from '@/components/TopTitle.vue';
import TableList from '@/components/TableList.vue';
@Component({
    components: {
        'top_title': TopTitle,
        'table_list': TableList,
    }
})
export default class PoplulationGraph extends Vue{
    graphShow(numArea: number) {

        //表で指定した値
        console.log(numArea);
    }
}
</script>