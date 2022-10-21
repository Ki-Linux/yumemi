<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  data() {
    return {
      chartData: {},
      options: {},
    }
  },
  mounted() {
    this.renderChart(this.chartData, this.options)
  },
}
</script>