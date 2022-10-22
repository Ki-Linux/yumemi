<template>
    <div>
        <div style="padding: 20px;">
            <p>都道府県</p>
            <label v-for="(area_data, index) in AreaData" :key="index">
                <input type="checkbox" name="area" @change="checkArea(index)" v-model="area_data.areaCheck">
                {{ area_data.areaName }}
            </label>
        </div>
    </div>
</template>
<script lang="ts">
import { Vue, Component } from 'vue-property-decorator';

@Component
export default class TableList extends Vue {
    AreaData: {areaNum: number; areaName: string; areaCheck: boolean;}[] = [];

    mounted() {

        //APIで呼び出し
        this.$axios.get(String(process.env.BASE_URL), 
        { headers: { 'X-API-KEY': process.env.API_KEY } })
            .then((res) => {
                const ResData = res.data.result;

                for(let i=0; i<ResData.length; i++) {

                    //APIからとってきたデータを代入
                    const prefC = JSON.parse(ResData[i].prefCode);
                    const prefN = ResData[i].prefName;

                    //localStorageにある値なのかを定義
                    let storageJudge = false;
                    const storageNum = localStorage.getItem(prefN);

                    //localStorageにあったらtrueにする
                    if(storageNum !== null) {
                        storageJudge = true;
                    }

                    //都道府県名とコード番号とlocalStorageにあるかないかの判断を配列に入れる
                    this.AreaData.push({areaNum: prefC, areaName: prefN, areaCheck: storageJudge});
                }
            })
            .catch((err) => {
                console.log(err);
            });
    }

    checkArea(indexNum: number) {//クリックした都道府県のコード番号取得

        const dataArea = this.AreaData[indexNum];

        //チェック外したら削除
        const keyNum = localStorage.getItem(dataArea.areaName);
        if(keyNum !== null) {//localstorageに指定した値があれば削除する
            localStorage.removeItem(dataArea.areaName);
            location.reload();
            return;
        }

        //追加
        localStorage.setItem(dataArea.areaName, String(dataArea.areaNum));

        //リロード
        location.reload();
    }
}
</script>