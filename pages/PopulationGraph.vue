<template>
    <top_title/>
</template>
<script lang="ts">
import { Vue, Component } from 'nuxt-property-decorator';
import TopTitle from '@/components/TopTitle.vue';
@Component({
    components: {
        'top_title': TopTitle,
    }
})
export default class PoplulationGraph extends Vue{
    i: string = "io";
}
</script>