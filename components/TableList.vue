<template>
    <div>
        <div>
            <p>都道府県</p>
            <label v-for="(area_data, index) in AreaData" :key="index">
                <input type="checkbox" name="area" :value=index>
                {{ area_data.areaName }}
            </label>
        </div>
    </div>
</template>
<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class TableList extends Vue {
    AreaData: {areaNum: number; areaName: string;}[] = [];

    mounted() {

        //APIで呼び出し
        this.$axios.get(String(process.env.BASE_URL), 
        { headers: { 'X-API-KEY': process.env.API_KEY } })
            .then((res) => {
                const ResData = res.data.result;

                for(let i=0; i<ResData.length; i++) {

                    const prefC = JSON.parse(ResData[i].prefCode);
                    const prefN = ResData[i].prefName;

                    //都道府県名とコード番号を配列に入れる
                    this.AreaData.push({areaNum: prefC, areaName: prefN});
                }

            })
            .catch((err) => {
                console.log(err);
            });
    }
}
</script>