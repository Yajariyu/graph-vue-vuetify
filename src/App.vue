<template>
  <v-app>
    <v-container>
        <Graph :data="data" />
    </v-container>
  </v-app>
</template>

<script>
import Graph from './components/Graph';

export default {
  name: 'App',
  components: {
    Graph
  },

  data(){
    return {
      data:  {
        datasets: 
        //Data to be consumed from an API (or Data resource)
          [{"userid": "55", "scores": [{"score": 50, "date": "2020-11-01 10:57:34"}, 
                                            {"score": 100, "date": "2020-11-05 10:57:34"}, 
                                            {"score": 150, "date": "2020-11-15 10:57:34"}]},
                {"userid": "12", "scores": [{"score": 66, "date": "2020-08-01 11:57:34"}, 
                                            {"score": 32, "date": "2020-10-05 10:57:34"},
                                            {"score": 12, "date": "2020-12-15 10:57:34"}]},
                {"userid": "80", "scores": [{"score": 20, "date": "2020-11-01 10:57:34"}, 
                                            {"score": 30, "date": "2020-11-05 10:57:34"}, 
                                            {"score": 40, "date": "2020-11-15 10:57:34"}]},
                {"userid": "34", "scores": [{"score": 200, "date": "2020-07-01 11:57:34"}, 
                                            {"score": 60, "date": "2020-10-05 10:57:34"},
                                            {"score": 20, "date": "2020-12-15 10:57:34"}]},
                {"userid": "10", "scores": [{"score": 90, "date": "2020-09-01 10:57:34"}, 
                                            {"score": 100, "date": "2020-11-05 10:57:34"}, 
                                            {"score": 125, "date": "2020-11-15 10:57:34"}]},
                {"userid": "20", "scores": [{"score": 80, "date": "2020-09-01 11:57:34"}, 
                                            {"score": 40, "date": "2020-10-05 10:57:34"},
                                            {"score": 30, "date": "2020-10-12 10:57:34"},
                                            {"score": 20, "date": "2020-10-13 10:57:34"},
                                            {"score": 10, "date": "2020-10-15 10:57:34"}]},
                {"userid": "30", "scores": [{"score": 46, "date": "2020-09-01 10:57:34"}, 
                                            {"score": 79, "date": "2020-11-05 10:57:34"}, 
                                            {"score": 150, "date": "2020-11-15 10:57:34"}]},
                {"userid": "60", "scores": [{"score": 213, "date": "2020-09-01 11:57:34"}, 
                                            {"score": 13, "date": "2020-10-05 10:57:34"},
                                            {"score": 3, "date": "2020-12-20 10:57:34"},
                                            {"score": 1, "date": "2020-12-28 10:57:34"}]},
          ] 
      }
    }
  }
}
</script>
