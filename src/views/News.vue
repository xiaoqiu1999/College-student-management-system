<!-- =========================================================================================
  File Name: DashboardAnalytics.vue
  Description: Dashboard Analytics
  ----------------------------------------------------------------------------------------
  Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
  Author: Pixinvent
  Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->

<template>
  <div id="notice-allnews">
    <div class="vx-row">
      <!-- CARD 1: CONGRATS -->
      <div class="vx-col w-full lg:w-1/2 mb-base">
        <vx-card
          slot="no-body"
          class="text-center bg-primary-gradient greet-user"
        >
          <img
            src="@/assets/images/elements/decore-left.png"
            class="decore-left"
            alt="Decore Left"
            width="200"
          />
          <img
            src="@/assets/images/elements/decore-right.png"
            class="decore-right"
            alt="Decore Right"
            width="175"
          />
          <feather-icon
            icon="AwardIcon"
            class="p-6 mb-8 bg-primary inline-flex rounded-full text-white shadow"
            svgClasses="h-8 w-8"
          ></feather-icon>
          <h1 class="mb-6 text-white">
            欢迎您 &nbsp;{{ checkpointReward.userName
            }}{{ checkpointReward.identity }},
          </h1>
          <p class="xl:w-3/4 lg:w-4/5 md:w-2/3 w-4/5 mx-auto text-white">
            你还有
            <strong>{{ checkpointReward.progress }}</strong>
            条未读通知，请尽快查阅！
          </p>
        </vx-card>
      </div>

      <!-- CARD 2: SUBSCRIBERS GAINED -->
      <div class="vx-col w-full sm:w-1/2 md:w-1/2 lg:w-1/4 xl:w-1/4 mb-base">
        <statistics-card-line
          icon="UsersIcon"
          :statistic="checkpointReward.department"
          :statisticTitle="checkpointReward.major"
          :studentId="checkpointReward.studentId"
          :chartData="subscribersGained.series"
          type="area"
        ></statistics-card-line>
      </div>

      <!-- CARD 3: ORDER RECIEVED -->
      <div class="vx-col w-full sm:w-1/2 md:w-1/2 lg:w-1/4 xl:w-1/4 mb-base">
        <statistics-card-line
          icon="ShoppingBagIcon"
          statistic="97.5K"
          statisticTitle="Orders Received"
          :chartData="ordersRecevied.series"
          color="warning"
          type="area"
        ></statistics-card-line>
      </div>
    </div>

    <div class="vx-row">
      <!-- CARD 4: SESSION -->
      <div class="vx-col w-full md:w-1/2 mb-base">
        <vx-card title="通知">
          <template slot="actions">
            <change-time-duration-dropdown />
          </template>
          <div
            class="vx-row flex-col-reverse md:flex-col-reverse sm:flex-row lg:flex-row"
          >
            <!-- LEFT COL -->
            <div
              class="vx-col w-full md:w-full sm:w-1/3 lg:w-1/3 xl:w-1/3 flex flex-col justify-between"
              v-if="salesBarSession.newsData"
            >
              <div>
                <!-- Previous Data Comparison -->
                <p class="mt-2 text-xl font-medium">
                  <span class="text-success">
                    <span v-if="salesBarSession.newsData.comparison.result > 0"
                      >+</span
                    >
                    <span>{{
                      salesBarSession.newsData.comparison.result
                    }}</span>
                  </span>
                  <span> 新通知 </span>
                  <span>在{{ salesBarSession.newsData.comparison.str }}</span>
                </p>
              </div>
              <img src="../assets/images/news1.png" class="w-full" alt="" />
            </div>

            <!-- RIGHT COL -->

            <div
              class=" h-48 overflow-auto vx-col w-full md:w-full sm:w-2/3 lg:w-2/3 xl:w-2/3 flex flex-col lg:mb-0 md:mb-base sm:mb-0 mb-base"
            >
              <a
                v-for="(item, index) in salesBarSession.newsData.newsList"
                :href="item.url"
                :key="index"
              >
                <div class="flex justify-between">
                  <div>
                    <feather-icon
                      icon="BellIcon"
                      svgClasses="h-4 w-4"
                    ></feather-icon>
                    <span>{{ item.description }}</span>
                  </div>
                  <span>{{ item.time }}</span>
                </div>
              </a>
              <vs-button
                icon-pack="feather"
                icon="icon-chevrons-right"
                icon-after
                class="shadow-md w-full lg:mt-0 mt-4"
                >查看更多</vs-button
              >
            </div>
          </div>
          <vs-divider class="my-6"></vs-divider>
          <!-- <div class="vx-row">
            <div class="vx-col w-1/2 mb-3">
              <p>Goal: $100000</p>
              <vs-progress class="block mt-1" :percent="50" color="primary"></vs-progress>
            </div>
            <div class="vx-col w-1/2 mb-3">
              <p>Users: 100K</p>
              <vs-progress class="block mt-1" :percent="60" color="warning"></vs-progress>
            </div>
            <div class="vx-col w-1/2 mb-3">
              <p>Retention: 90%</p>
              <vs-progress class="block mt-1" :percent="70" color="danger"></vs-progress>
            </div>
            <div class="vx-col w-1/2 mb-3">
              <p>Duration: 1yr</p>
              <vs-progress class="block mt-1" :percent="90" color="success"></vs-progress>
            </div>
          </div> -->
        </vx-card>
      </div>

      <!-- CARD 5: SUPPORT TRACKER -->
      <div class="vx-col w-full md:w-1/2 lg:w-1/2 xl:w-1/2 mb-base">
        <vx-card title="消息">
          <!-- CARD ACTION -->
          <template slot="actions">
            <change-time-duration-dropdown />
          </template>

          <div slot="no-body" v-if="message.analyticsData">
            <div class="vx-row text-center">
              <!-- Open Tickets Heading -->
              <div
                class="vx-col w-full lg:w-1/5 md:w-full sm:w-1/5 flex flex-col justify-between mb-4 lg:order-first md:order-last sm:order-first order-last"
              >
                <div class="lg:ml-6 lg:mt-6 md:mt-0 md:ml-0 sm:ml-6 sm:mt-6">
                  <h1 class="font-bold text-5xl">
                    {{ message.analyticsData.allTickets }}
                  </h1>
                  <small>全部消息</small>
                </div>
              </div>

              <!-- Chart -->
              <div
                class="vx-col w-full lg:w-4/5 md:w-full sm:w-4/5 justify-center mx-auto lg:mt-0 md:mt-6 sm:mt-0 mt-6"
              >
                <vue-apex-charts
                  type="radialBar"
                  height="385"
                  :options="analyticsData.supportTrackerRadialBar.chartOptions"
                  :series="messageType.series"
                />
              </div>
            </div>

            <!-- Support Tracker Meta Data -->
            <div class="flex flex-row justify-between px-8 pb-4 mt-4">
              <p
                class="text-center"
                v-for="(val, key) in message.analyticsData.meta"
                :key="key"
              >
                <span class="block">{{ messageType[key] }}</span>
                <span class="text-2xl font-semibold">{{ val }}</span>
              </p>
            </div>
          </div>
        </vx-card>
      </div>
    </div>
  </div>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'
import StatisticsCardLine from '@/components/statistics-cards/StatisticsCardLine.vue'
import analyticsData from './ui-elements/card/analyticsData.js'
import ChangeTimeDurationDropdown from '@/components/ChangeTimeDurationDropdown.vue'
import VxTimeline from '@/components/timeline/VxTimeline'

export default {
  data () {
    return {
      checkpointReward: {},
      subscribersGained: {},
      ordersRecevied: {},
      salesBarSession: {},
      message: {},
      productsOrder: {},
      salesRadar: {},
      messageType: {
        newMessage: '新消息',
        completedMessage: '已读消息',
        unreadMessage: '未读消息',
        series: []
      },

      analyticsData,
      dispatchedOrders: []
    }
  },
  components: {
    VueApexCharts,
    StatisticsCardLine,
    ChangeTimeDurationDropdown,
    VxTimeline
  },
  created () {
    //  User Reward Card
    this.$http
      .get('/api/user/checkpoint-reward')
      .then(response => {
        this.checkpointReward = response.data
      })
      .catch(error => {
        console.log(error)
      })

    // Subscribers gained - Statistics
    this.$http
      .get('/api/card/card-statistics/subscribers')
      .then(response => {
        this.subscribersGained = response.data
      })
      .catch(error => {
        console.log(error)
      })

    // Orders - Statistics
    this.$http
      .get('/api/card/card-statistics/orders')
      .then(response => {
        this.ordersRecevied = response.data
      })
      .catch(error => {
        console.log(error)
      })

    // Sales bar - Analytics
    this.$http
      .get('/api/card/card-analytics/sales/bar')
      .then(response => {
        this.salesBarSession = response.data
      })
      .catch(error => {
        console.log(error)
      })

    // Support Tracker
    this.$http
      .get('/api/card/card-analytics/support-tracker')
      .then(response => {
        this.message = response.data
        // 计算已阅读百分比
        this.messageType.series.push(
          (
            this.message.analyticsData.meta.completedMessage /
              this.message.analyticsData.allTickets
          ) * 100
        )
      })
      .catch(error => {
        console.log(error)
      })

    // Products Order
    this.$http
      .get('/api/card/card-analytics/products-orders')
      .then(response => {
        this.productsOrder = response.data
      })
      .catch(error => {
        console.log(error)
      })

    // Sales Radar
    this.$http
      .get('/api/card/card-analytics/sales/radar')
      .then(response => {
        this.salesRadar = response.data
      })
      .catch(error => {
        console.log(error)
      })

    // Dispatched Orders
    this.$http
      .get('/api/table/dispatched-orders')
      .then(response => {
        this.dispatchedOrders = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>

<style lang="scss">
/*! rtl:begin:ignore */
#notice-allnews {
  .greet-user {
    position: relative;

    .decore-left {
      position: absolute;
      left: 0;
      top: 0;
    }
    .decore-right {
      position: absolute;
      right: 0;
      top: 0;
    }
  }

  @media (max-width: 576px) {
    .decore-left,
    .decore-right {
      width: 140px;
    }
  }
}
/*! rtl:end:ignore */
</style>
