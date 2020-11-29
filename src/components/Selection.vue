<template>
    <div>
    <v-container fluid>
        <v-row >
            <v-col cols=10>
                <Chart :chartData="fillData" class="chart" />
            </v-col>
            <v-col cols=2 class="selector" >
                <v-checkbox   @click='all' :label="`All`" v-model="allSelected" class="all"/> 
                <v-item-group  no-gutters :key="user.userid" v-for="user in data_ar" class="items" >
                    <v-checkbox  @click="select" :id="user.userid" :value="user.userid" v-model=selected :color="user.color" v-bind:label="`User ${user.userid}`" class="item"/> 
                </v-item-group>
            </v-col>
        </v-row> 
    </v-container>     
    </div>
</template>

<script>

import Chart from './Chart.vue'
export default {
    name: 'Selection',
      components:{
    Chart },
    props:  {
        data: {
          type: Object,
          default: null
    },
  },
  data(){
    return {
      selected:[],
      data_ar:[],
      user:[],
      color:['#F44336','#CE93D8','#90CAF9','#9E9D24','#1B5E20','#FF9800','#795548','#9CCC65','#76FF03','#827717','#01579B','#5E35B1'], //Define List of Color to be Used in Chart
      users:[],
      allSelected:false
    }
  },

  watch: {
      selected() {     
         this.users= this.data_ar.filter((user)=> { 
          return this.selected.includes(user.userid)
        })   
      },
  },
  mounted(){
    this.data_ar=JSON.parse(JSON.stringify(this.data.datasets))
    let color_i=-1;
    this.data_ar.forEach(user => {
      color_i= this.color_index(color_i)
      user['color']=this.color[color_i]  
    });
  },

  methods:{
    color_index:function (color_index) {
      if (color_index>=this.color.length-1) { return 0 }
      return color_index+=1
    },

    dates:function(dates_all){
      return dates_all.sort(this.order_date);
  },
    order_date:function(a,b){
        return new Date(a)-new Date(b);
    },

    all:function(){
        this.selected=[]
        if(this.allSelected) {
        this.data_ar.forEach((user)=>{
          this.selected.push(user.userid)
        })
        }

        return this.selected
    },
    select:function(){
      this.allSelected=false
    }

  },
  computed: {
    fillData: function () {
      let scores=[];
      let chartdata={
        datasets:[],
        labels:[]
      }

    //Format data to Chart
      for (const user in this.users) {
      scores=[];
          for (const info in this.users[user].scores) {
            let date=this.users[user].scores[info].date.split(" ")[0];
            scores.push({x:date,
                     y:this.users[user].scores[info].score})
             
          }
        chartdata['datasets'].push(
                                  {label:'user'+(this.users[user].userid),
                                  borderWidth: 2,
                                  pointBackgroundColor: "white",
                                  data:scores,
                                  fill: false,
                                  borderColor:this.users[user].color
                                   })
      }
      
      //Return data formatted to Chart 
      return chartdata
      
    },  

    },
}
</script>

<style>
    .selector{
        overflow: scroll;
    }

    .selector, .chart{
         height: 75vh;
    }
    .item, .all {
        height:20px
    }
    .item, .items{
        padding: 0px;
        margin:0px;
    }
</style>