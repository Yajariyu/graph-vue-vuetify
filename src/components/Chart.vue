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
                      unit:'month'
                        },

              },
            
        ]},
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
