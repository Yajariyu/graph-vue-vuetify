<template>
<div>
  <v-container fluid>
     <v-row >
    <v-col
      cols=10>
    <Chart :chartData="fillData" />
    </v-col>
    <v-col 
      cols=2 class="selector" >
      <v-checkbox   @click='all' :label="`All`" v-model="allSelected"/> 
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
// import vuescroll from 'vuescroll';
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
      let dates=[];
      let dates_first=[];
      let dates_last=[];
      let size='';
      let max_index=null;
      let size_bigger=0;


      let chartdata={
        datasets:[],
        labels:[]
      }
      

      for (const user in this.users) {
        size=this.users[user].scores.length;
        size_bigger=size_bigger > size? size_bigger:size;
        max_index=user 
      }

      for (const user in this.users) {
        size=this.users[user].scores.length;
        const date_initial=this.users[user].scores[0].date.split(" ")[0];
        const date_last=this.users[user].scores[size-1].date.split(" ")[0]
        if(!(dates_first.includes(date_initial))) {
          dates_first.push(date_initial);
        }
        if(!(dates_last.includes(date_last))) {
          dates_last.push(date_last);
        } 
    /*  size_bigger=size_bigger > size? size_bigger:size;
      dates= size_bigger > size ? dates :  [];
      let change = size_bigger > size ?false :true;   */ 
      scores=[];
      for (const info in this.users[user].scores) {
                let date=this.users[user].scores[info].date.split(" ")[0];
                if (max_index==user) {
                  dates.push(date);
                }
                scores.push({x:date,
                            y:this.users[user].scores[info].score})
             
      }
         console.log(scores)  
              chartdata['datasets'].push(
                                        {label:'user'+(this.users[user].userid),
                                        borderWidth: 2,
                                        pointBackgroundColor: "white",
                                        data:scores,
                                        fill: false,
                                        borderColor:this.users[user].color
                                        })
      }

      dates_first=this.dates(dates_first);
      dates_last=this.dates(dates_last);
      if(dates_first[0]){
        dates[0]=dates_first[0];
      }
      if(dates_last[0]){
        dates.pop();
        dates.push(...dates_last)
      }

    /*  chartdata['labels']=dates */ 
      return chartdata
      
    },

  

    },
}
</script>

<style>
.selector{
   overflow: scroll;
}

.item{
  padding: 3px;
  margin:0px;
}
</style>