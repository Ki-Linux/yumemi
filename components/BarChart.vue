<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  data() {
    return {

    chartColor: [
        '#00FFFF',//北海道
        '#4169E1',//青森
        '#2F4F4F',//岩手
        '#00008B',//宮城
        '#008BBB',//秋田
        '#5F9EA0',//山形
        '#6B8E23',//福島
        '#7FFFD4',//茨城
        '#8B008B',//栃木
        '#8B0000',//群馬
        '#DC143C',//埼玉
        '#BC8F8F',//千葉
        '#FF4500',//東京
        '#B8860B',//神奈川
        '#F0E68C',//新潟
        '#FFDAB9',//富山
        '#CD5C5C',//石川
        '#B0C4DE',//福井
        '#708090',//山梨
        '#191970',//長野
        '#4682B4',//岐阜
        '#20B2AA',//静岡
        '#556B2F',//愛知
        '#00FA9A',//三重
        '#6A5ACD',//滋賀
        '#8B4513',//京都
        '#FF1493',//大阪
        '#C71585',//兵庫
        '#FF6347',//奈良
        '#CD853F',//和歌山
        '#EEE8AA',//鳥取
        '#F5DEB3',//島根
        '#FFD770',//岡山
        '#3CB371',//広島
        '#778899',//山口
        '#483D8B',//徳島
        '#1E90FF',//香川
        '#66CDAA',//愛媛
        '#006400',//高知
        '#00FF7F',//福岡
        '#8A2BE2',//佐賀
        '#A52A2A',//長崎
        '#FF69B4',//熊本
        '#DB7093',//大分
        '#FF4F50',//宮崎
        '#DAA520',//鹿児島
        '#FFD700',//沖縄
    ],

    chartData: {labels: ["1980", "1990", "2000", "2010", "2020"],

    //ここにAPIからとってきたデータを入れる
    datasets: [
    ]},
      options: {
        scales: {//x軸,y軸ののタイトル表示とy軸の幅
            xAxes: [{
                scaleLabel: {
                    display: true,
                    labelString: '年度'
                }
            }],
            yAxes: [{
                scaleLabel: {
                    display: true,
                    labelString: '人口数'
                }
            }]
        }
      },
    }
  },
  mounted() {

    for(let i=0; i<localStorage.length; i++) {
        const ItemKey = localStorage.key(i);
        const Item = localStorage.getItem(ItemKey);

        //APIを使ってグラフに示すデータを取ってくる
        this.$axios.get(String(process.env.GRAPH_URL) + Item, 
        { headers: { 'X-API-KEY': process.env.API_KEY } })
            .then((res) => {
                const detailData = res.data.result.data[0].data;

                this.chartData.datasets.push({
                    label: ItemKey,//県名
                    data: [
                        detailData[4].value, 
                        detailData[6].value, 
                        detailData[8].value, 
                        detailData[10].value, 
                        detailData[12].value
                    ],
                    borderColor: this.chartColor[Item-1],//'rgba(255, 100, 100, 1)',
                    backgroundColor: "rgba(0,0,0,0)"
                });
                this.renderChart(this.chartData, this.options)
            })
            .catch((err) => {
                console.log(err);
            });
    } 
  },
}
</script>