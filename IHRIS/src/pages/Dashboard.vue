<template>
  <div>

    <div class="row">
      <div class="col-12">
        <card type="chart">
          <template slot="header">
            <div class="row">
              <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
                <h2 class="card-title">{{$t('dashboard.performance')}}</h2>
              </div>

              <!-- First Graph -->
              <div class="col-sm-6">
                <div class="btn-group btn-group-toggle"
                     :class="isRTL ? 'float-left' : 'float-right'"
                     data-toggle="buttons">    
                  <label v-for="(option, index) in bigLineChartCategories"
                         :key="option"
                         class="btn btn-sm btn-primary btn-simple"
                         :class="{active: bigLineChart.activeIndex === index}"
                         :id="index">
                    <input type="radio"
                           @click="initBigChart(index)"
                           name="options" autocomplete="off"
                           :checked="bigLineChart.activeIndex === index">
                    {{option}}
                  </label>
                </div>
              </div>
            </div>
          </template>
          <div class="chart-area">
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
    </div>
    <div class="row">
      
      <div class="col-lg-6" :class="{'text-right': isRTL}">
        <card type="chart">
          <template slot="header">
            <h5 class="card-category">{{$t('dashboard.healthPerRegion')}}</h5>
              
          </template>
          <div class="chart-area">

            <!-- Third Graph -->
            <bar-chart style="height: 100%"
                       chart-id="blue-bar-chart"
                       :chart-data="blueBarChart.chartData"
                       :gradient-stops="blueBarChart.gradientStops"
                       :extra-options="blueBarChart.extraOptions">
            </bar-chart>
          </div>
        </card>
      </div>
      <div class="col-lg-6" :class="{'text-right': isRTL}">
        <card type="chart">
          
          <template slot="header">
            <div class="row">
              <div class="col-lg-6">
                <h5 class="card-category">{{$t('dashboard.cadrePerRegion')}}</h5>
              </div>

              <div class="col-lg-6 "> 
                <label for="cadre"> Choose Cadre : </label>
                <select name="Cadre btn-group btn-group-toggle" id="cadre">
                  <option value="Health Officer" class="btn btn-sm btn-simple"> Health Officer</option>
                  <option value="Health Officer" class="btn btn-sm btn-simple"> Chief Officer</option>
                  <option value="Health Officer" class="btn btn-sm btn-simple"> HR Officer</option>
                  
                </select>
              </div>
            </div>


          </template>
          <div class="chart-area">

            <!-- Fourth Graph -->
            <bar-chart style="height: 100%"
                        chart-id="green-line-chart"
                        :chart-data="greenLineChart.chartData"
                        :gradient-stops="greenLineChart.gradientStops"
                        :extra-options="greenLineChart.extraOptions">
            </bar-chart>
          </div>
        </card>
      </div>
    </div>
    <div class="row">
      <div class="col-lg-6 col-md-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title">{{$t('dashboard.cadreTable')}}</h4>
          <div class="table-responsive">
            <task-list></task-list>
          </div>
        </card>
      </div>
      <div class="col-lg-6 col-md-12">
        <card class="card" :header-classes="{'text-right': isRTL}">
          <h4 slot="header" class="card-title">{{$t('dashboard.facilityTable')}}</h4>
          <div class="table-responsive">
            <user-table></user-table>
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
  import config from '@/config';

  export default {
    components: {
      LineChart,
      BarChart,
      TaskList,
      UserTable
    },
    data() {
      return {
        bigLineChart: {
          allData: [
            [2001, 2005, 2003, 2005, 2007, 2010, 2015, 2006, 2009, 2016, 2011, 2017],
            [2011, 2003, 2001, 2010, 2008, 2013, 2015, 2006, 2001, 2009, 2016, 2005],
            [2009, 2005, 2010, 2015, 2003, 2007, 2011, 2001, 2013, 2006, 2007, 2012]
          ],
          activeIndex: 0,
          chartData: {
            datasets: [{ }],
            
            labels: ['Kakamega', 'Migori', 'Nairobi', 'Meru', 'Kitale', 'Kilifi', 'Malindi', 'Kisumu', 'Voi', 'Mombasa', 'Nyeri', 'Turkana'],
          },
          
          extraOptions: chartConfigs.purpleChartOptions,
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          categories: []
        },
        purpleLineChart: {
          extraOptions: chartConfigs.purpleChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'],
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
              data: [80, 100, 70, 80, 120, 80],
            }],
              
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        greenLineChart: {
          extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: ['Kach', 'Mig', 'Nai', 'Meru', 'Kit', 'Kil', 'Mal', 'Kis', 'Voi', 'Mom', 'Nyr', 'Tur'],
            datasets: [{
              label: "Cadre",
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
              data: [15, 17, 3, 10, 16, 9, 11, 7, 9, 5, 12, 4],
            }]
          },
          gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
          gradientStops: [1, 0.4, 0],
        },
        blueBarChart: {
          extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: ['Kach', 'Mig', 'Nai', 'Meru', 'Kit', 'Kil', 'Mal', 'Kis', 'Voi', 'Mom', 'Nyr', 'Tur'],
            datasets: [{
              label: "Health Workers",
              fill: true,
              borderColor: config.colors.info,
              borderWidth: 2,
              borderDash: [],
              borderDashOffset: 0.0,
              data: [53, 20, 10, 33, 67, 45, 27, 54, 12, 34, 23, 45],
            }]
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        }
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
      }
    },
    methods: {
      initBigChart(index) {
        let chartData = {
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
            data: this.bigLineChart.allData[index],
          }],
          options: this.bigLineChart.options,
          labels: ['Kakamega', 'Migori', 'Nairobi', 'Meru', 'Kitale', 'Kilifi', 'Malindi', 'Kisumu', 'Voi', 'Mombasa', 'Nyeri', 'Turkana'],
        }
        let options = {
            scales: {
                yAxes: [{
                    ticks: {
                        beginAtZero:false
                    },
                    scaleLabel: {
                        display: true,
                        labelString: 'Temperature'
                    },
                    scaleOverride: true,
                    scaleSteps: 1000,
                    scaleStepWidth: 10,
                    scaleStartValue: 2000
                }]
            },
          }
        this.$refs.bigChart.updateGradients(chartData);
        this.bigLineChart.chartData = chartData;
        this.bigLineChart.activeIndex = index;
        this.bigLineChart.options=options
      }
    },
    mounted() {
      this.i18n = this.$i18n;
      if (this.enableRTL) {
        this.i18n.locale = 'ar';
        this.$rtl.enableRTL();
      }
      this.initBigChart(0);
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
