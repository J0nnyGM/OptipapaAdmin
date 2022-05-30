<template>
  <div>
    <div class="row">
      <div class="col-12">
        <card type="chart">
          <template slot="header">
            <div class="row">
              <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                <h2 class="card-title">{{$t('Usuarios Registrados')}}</h2>
              </div>
            </div>
          </template>
          <div class="chart-area" :key="keyBigChart">
            <line-chart style="height: 100%"
                        ref="bigChart"
                        chart-id="big-line-chart"
                        :chart-data="bigLineChart.chartData"
                        :gradient-colors="bigLineChart.gradientColors"
                        :gradient-stops="bigLineChart.gradientStops"
                        :extra-options="bigLineChart.extraOptions">
            </line-chart>
          </div>
        </card>
      </div>

      <div class="col-12">
        <card type="chart">
          <template slot="header">
            <div class="row">
              <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                <h2 class="card-title">{{$t('Cultivos Registrados')}}</h2>
              </div>
            </div>
          </template>
          <div class="chart-area" :key="keyBigChartCultivos">
            <line-chart style="height: 100%"
                        ref="bigChart"
                        chart-id="big-line-chart"
                        :chart-data="bigLineChartCultivos.chartData"
                        :gradient-colors="bigLineChartCultivos.gradientColors"
                        :gradient-stops="bigLineChartCultivos.gradientStops"
                        :extra-options="bigLineChartCultivos.extraOptions">
            </line-chart>
          </div>
        </card>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart">
          <template slot="header">
            <h5 class="card-category">Calificaciones de la aplicacion por usuarios</h5>
            <h3 class="card-title"><i class="tim-icons icon-bell-55 text-primary "></i> Limitado a 5 usuarios</h3>
          </template>
          <div class="chart-area" :key="purpleLineChartKey">
            <line-chart style="height: 100%"
                        chart-id="purple-line-chart"
                        :chart-data="purpleLineChart.chartData"
                        :gradient-colors="purpleLineChart.gradientColors"
                        :gradient-stops="purpleLineChart.gradientStops"
                        :extra-options="purpleLineChart.extraOptions">
            </line-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart">
          <template slot="header">
            <h5 class="card-category">Promedio de tiempo de cultivos en semanas</h5>
            <h3 class="card-title"><i class="tim-icons icon-delivery-fast text-info "></i> Limitado a 5</h3>
          </template>
          <div class="chart-area" :key="blueBarChartKey">
            <bar-chart style="height: 100%"
                       chart-id="blue-bar-chart"
                       :chart-data="blueBarChart.chartData"
                       :gradient-stops="blueBarChart.gradientStops"
                       :extra-options="blueBarChart.extraOptions">
            </bar-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-4" :class="{'text-right': isRTL}">
        <card type="chart">
          <template slot="header">
            <h5 class="card-category">Promedio De Agua De Cultivos En Semanas</h5>
            <h3 class="card-title"><i class="tim-icons icon-send text-success "></i> Limitado a 5</h3>
          </template>
          <div class="chart-area" :key="greenLineBartKey">
            <line-chart style="height: 100%"
                        chart-id="green-line-chart"
                        :chart-data="greenLineChart.chartData"
                        :gradient-stops="greenLineChart.gradientStops"
                        :extra-options="greenLineChart.extraOptions">
            </line-chart>
          </div>
        </card>
      </div>
    </div>

  </div>
</template>
<script>
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';
  import * as chartConfigs from '@/components/Charts/config';
  import TaskList from './Dashboard/TaskList';
  import UserTable from './Dashboard/UserTable';
  import { BaseTable } from "@/components";
  import config from '@/config';
  import Axios from 'axios';


  export default {
    components: {
      LineChart,
      BaseTable,
      BarChart,
      TaskList,
      UserTable
    },
    data() {
      return {
        blueBarChartKey:0,
        greenBarChartKey:0,
        purpleLineChartKey:0,
        greenLineBartKey:0,
        keyBigChart:0,
        keyBigChartCultivos:0,
        dates:[],
        datesCultivos:[],
        bigLineChart: {
          activeIndex: 0,
          chartData: {
            datasets: [{
            fill: true,
            borderColor: config.colors.primary,
            borderWidth: 2,
            borderDash: [],
            borderDashOffset: 0.0,
            pointBackgroundColor: config.colors.primary,
            pointBorderColor: 'rgba(255,255,255,0)',
            pointHoverBackgroundColor: config.colors.primary,
            pointBorderWidth: 20,
            pointHoverRadius: 4,
            pointHoverBorderWidth: 15,
            pointRadius: 4,
            data: [],
          }],
            labels: [],
          },
          extraOptions: chartConfigs.purpleChartOptions,
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          categories: []
        },
        bigLineChartCultivos: {
          activeIndex: 0,
          chartData: {
            datasets: [{
            fill: true,
            borderColor: config.colors.primary,
            borderWidth: 2,
            borderDash: [],
            borderDashOffset: 0.0,
            pointBackgroundColor: config.colors.primary,
            pointBorderColor: 'rgba(255,255,255,0)',
            pointHoverBackgroundColor: config.colors.primary,
            pointBorderWidth: 20,
            pointHoverRadius: 4,
            pointHoverBorderWidth: 15,
            pointRadius: 4,
            data: [],
          }],
            labels: [],
          },
          extraOptions: chartConfigs.purpleChartOptions,
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          categories: []
        },
        purpleLineChart: {
          extraOptions: chartConfigs.purpleChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Data",
              fill: true,
              borderColor: config.colors.primary,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.primary,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.primary,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        greenLineChart: {
          extraOptions: chartConfigs.greenChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Water",
              fill: true,
              borderColor: config.colors.danger,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              pointBackgroundColor: config.colors.danger,
              pointBorderColor: 'rgba(255,255,255,0)',
              pointHoverBackgroundColor: config.colors.danger,
              pointBorderWidth: 20,
              pointHoverRadius: 4,
              pointHoverBorderWidth: 15,
              pointRadius: 4,
              data: [],
            }]
          },
          gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
          gradientStops: [1, 0.4, 0],
        },
        blueBarChart: {
          extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: [],
            datasets: [{
              label: "Countries",
              fill: true,
              borderColor: config.colors.info,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
      }
    },
    computed: {
      enableRTL() {
        return this.$route.query.enableRTL;
      },
      isRTL() {
        return this.$rtl.isRTL;
      },
      bigLineChartCategories() {
        return this.$t('dashboard.chartCategories');
      },
    
    },
    methods: {
      calculateBigChartData(){
        let numbers = [];
        let temp = [];
        this.dates.forEach((value,index)=>{
          let toAdd = true;
          for(const dateTemp of temp){
           if(dateTemp==value){
            temp.forEach((value,index)=>{
              if(dateTemp==value){
                toAdd = false;
                numbers[index]++
              }
            });
           } 
          }
          if(toAdd){
             temp.push(value)
             numbers.push(1);
           }
        });
        this.bigLineChart.chartData.labels = temp;
        this.bigLineChart.chartData.datasets[0].data = numbers;
        this.keyBigChart++;
        this.keyBigChartCultivos++;
        this.purpleLineChartKey++;
        this.blueBarChartKey++;
      },
      calculateBigChartDataCultivos(){
        let numbers = [];
        let temp = [];
        this.datesCultivos.forEach((value,index)=>{
          let toAdd = true;
          for(const dateTemp of temp){
           if(dateTemp==value){
            temp.forEach((value,index)=>{
              if(dateTemp==value){
                toAdd = false;
                numbers[index]++
              }
            });
           } 
          }
          if(toAdd){
             temp.push(value)
             numbers.push(1);
           }
        });
        this.bigLineChartCultivos.chartData.labels = temp;
        this.bigLineChartCultivos.chartData.datasets[0].data = numbers;
        this.greenLineBartKey++;

}
    },
    beforeMount(){
      Axios.get("https://optipapa-c3caa-default-rtdb.firebaseio.com/users.json").then((value)=>{
        let data = value.data;
                
        for(var key of Object.keys(data)){
          let currentObject = data[key];
          let user = {
            id:"",
            email:"",
            date:"",
            rating:0
          }
          user.id = currentObject.id;
          user.email = currentObject.email;
          user.date = currentObject.date;
          user.rating = currentObject.rating;

          if(this.purpleLineChart.chartData.labels.length<6){
            this.purpleLineChart.chartData.labels.push(user.email);
            this.purpleLineChart.chartData.datasets[0].data.push(user.rating);
          }

          if(this.blueBarChart.chartData.labels.length<6){
            this.blueBarChart.chartData.labels.push(currentObject.cultivos[0].name);
            this.blueBarChart.chartData.datasets[0].data.push(currentObject.cultivos[0].time);
          }

          if(this.greenLineChart.chartData.labels.length<6){
            console.log(currentObject.cultivos[0].water);
            this.greenLineChart.chartData.labels.push(currentObject.cultivos[0].name);
            this.greenLineChart.chartData.datasets[0].data.push(currentObject.cultivos[0].water);
          }

          this.dates.push(currentObject.date);
          this.datesCultivos.push(currentObject.cultivos[0].date);
        }

        this.calculateBigChartData();                   
        this.calculateBigChartDataCultivos();
      }).catch((error)=>{
        console.log(error);
      });
    },
    mounted() {
      this.i18n = this.$i18n;
      if (this.enableRTL) {
        this.i18n.locale = 'ar';
        this.$rtl.enableRTL();
      }
    },
    beforeDestroy() {
      if (this.$rtl.isRTL) {
        this.i18n.locale = 'en';
        this.$rtl.disableRTL();
      }
    }
  };
</script>
<style>
</style>
