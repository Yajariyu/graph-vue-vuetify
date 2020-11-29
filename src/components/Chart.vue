<script>
import { Line, mixins } from 'vue-chartjs'
const { reactiveProp } = mixins;

export default {
  extends: Line,

  mixins: [reactiveProp],
  name: 'Chart',
  props: ['chartData'],
  data(){
    return {
    options: {
      hover: {
          mode: "x"
        },
        scales: {
            xAxes: [{
                 type: 'time',
                 time: {
                      unit:'week' //Time could be change 'month'
                        },

                    },]},
        responsive: true, maintainAspectRatio: false ,
        tooltips: {
            mode: 'point'
        }
      },

    }
  },
      
  mounted () {
     this.renderChart(this.chartData,this.options);
  },


  
}
</script>

