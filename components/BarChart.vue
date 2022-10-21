<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  data() {
    return {
      chartData: {labels: ["1980", "1990", "2000", "2010", "2020"],

    //ここにAPIからとってきたデータを入れる
    datasets: [{
        label: '人口数',//県名
        data: [1500, 1600, 1700, 1800, 1900],
        borderColor: 'rgba(255, 100, 100, 1)',
        backgroundColor: "rgba(0,0,0,0)"
    },{
        label: '人口数',//県名
        data: [1500, 1600, 1700, 1800, 2000],
        borderColor: 'blue',
        backgroundColor: "rgba(0,0,0,0)",
    },
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
                },
                ticks: {
                    suggestedMax: 2000,
                    suggestedMin: 1500,
                    stepSize: 50,
                }
            }]
        }
      },
    }
  },
  mounted() {
    this.renderChart(this.chartData, this.options)
  },
}
</script>