<template>
  <div>
    <!--置顶新闻 -->
    <a
      class="sticky bg-white p-3 m-3 d-flex"
      :href="data.statistics.marquee[0].marqueeLink"
    >
      <div class="wrapper flex-1">
        <span class="label">{{ data.statistics.marquee[0].marqueeLabel }}</span>
        <span class="px-4 content">{{
          data.statistics.marquee[0].marqueeContent
        }}</span>
      </div>
      <span class="iconfont icon-arrow"></span>
    </a>

    <!-- 数据 -->
    <m-card class="data" title="全国数据统计">
      <el-card class="box-card">
        <div class="row1 d-flex jc-around pb-3">
          <div class="item1 d-flex flex-column  ai-center jc-around">
            <div>
              较昨日
              <span class="cci"
                >+{{ data.statistics.currentConfirmedIncr }}</span
              >
            </div>
            <strong class="ccc">{{
              data.statistics.currentConfirmedCount
            }}</strong>
            <strong class="text">现存确诊</strong>
          </div>

          <div class="item2 d-flex flex-column ai-center jc-around">
            <div>
              较昨日
              <span class="cci">+{{ data.statistics.suspectedIncr }}</span>
            </div>
            <strong class="ccc">{{ data.statistics.suspectedCount }}</strong>
            <strong class="text">现存疑似</strong>
          </div>

          <div class="item3 d-flex flex-column ai-center jc-around">
            <div>
              较昨日
              <span class="cci">+{{ data.statistics.curedIncr }}</span>
            </div>
            <strong class="ccc">{{ data.statistics.curedCount }}</strong>
            <strong class="text">治愈</strong>
          </div>
        </div>

        <div class="row2 d-flex jc-around">
          <div class="item1 d-flex flex-column ai-center jc-around">
            <div>
              较昨日
              <span class="cci">+{{ data.statistics.confirmedIncr }}</span>
            </div>
            <strong class="ccc">{{ data.statistics.confirmedCount }}</strong>
            <strong class="text">累计确诊</strong>
          </div>

          <div class="item2 d-flex flex-column ai-center jc-around">
            <div>
              较昨日
              <span class="cci">+{{ data.statistics.seriousIncr }}</span>
            </div>
            <strong class="ccc">{{ data.statistics.seriousCount }}</strong>
            <strong class="text">现存重症</strong>
          </div>

          <div class="item3 d-flex flex-column ai-center jc-around">
            <div>
              较昨日
              <span class="cci">+{{ data.statistics.deadIncr }}</span>
            </div>
            <strong class="ccc">{{ data.statistics.deadCount }}</strong>
            <strong class="text">死亡</strong>
          </div>
        </div>
      </el-card>
    </m-card>

    <!-- 地图 -->

    <myMap></myMap>
    <!-- 疫情图 -->
    <picCard title="全国" :items="data.statistics.quanguoTrendChart"> </picCard>
    <picCard title="湖北" :items="data.statistics.hbFeiHbTrendChart"> </picCard>

    <!-- Table -->
    <Table :items="data.listByArea"></Table>

    <!-- 实时播报 -->
    <div class="card bg-white p-3 mt-3">
      <div class="card-spheader d-flex ai-center pb-2">
        <div class="fs-xl flex-1 px-2">
          <div class="title">
            <strong class="px-2">实时播报</strong>
          </div>
        </div>
      </div>
    </div>
    <div
      class="news"
      v-for="(item, index) in data.timeline"
      :key="`${index} + 1`"
    >
      <newsCard :item="item"> </newsCard>
    </div>
  </div>
</template>

<script>
import picCard from "../components/picCard";
import myMap from "../components/myMap";
import newsCard from "../components/newsCard";
import Table from "../components/Table";
export default {
  data: function() {
    return {
      data: {
        statistics: {
          quanguoTrendChart: [],
          hbFeiHbTrendChart: [],
          marquee: [
            {
              marqueeLabel: "",
              marqueeContent: "",
              marqueeLink: ""
            }
          ],
          currentConfirmedCount: "",
          confirmedCount: "",
          suspectedCount: "",
          curedCount: "",
          deadCount: "",
          seriousCount: "",
          suspectedIncr: "",
          currentConfirmedIncr: "",
          confirmedIncr: "",
          curedIncr: "",
          deadIncr: "",
          seriousIncr: ""
        },
        timeline: [],
        listByArea: []
      },
      swiperOption: {
        pagination: {
          el: ".swiper-pagination",
          clickable: true
        }
      }
    };
  },
  methods: {
    async fetch() {
      const res = await this.$http.get(`/`);

      this.data = res.data.data;
    }
  },
  created() {
    this.fetch();
  },
  components: {
    picCard,
    newsCard,
    Table,
    myMap
  }
};
</script>

<style lang="scss">
@import "../assets/scss/variables";

.sticky {
  font-size: 1.2rem;
  .wrapper {
    .label {
      background-color: #ffefed;
      color: #f74c31;
    }
  }
}

.title-btn {
  width: calc(25%);
  word-wrap: break-word !important;
  word-break: break-all !important;
  white-space: normal !important;
}

.data {
  .row1 {
    .item1 {
      .cci {
        color: #f74c31;
      }
      .ccc {
        color: #f74c31;
        font: 1.5em sans-serif;
        font-weight: 700;
      }
    }

    .item2 {
      .cci {
        color: #f78207;
      }
      .ccc {
        color: #f78207;
        font: 1.5em sans-serif;
        font-weight: 700;
      }
    }

    .item3 {
      .cci {
        color: #28b7a3;
      }
      .ccc {
        color: #28b7a3;
        font: 1.5em sans-serif;
        font-weight: 700;
      }
    }
  }

  .row2 {
    .item1 {
      .cci {
        color: #ae212c;
      }
      .ccc {
        color: #ae212c;
        font: 1.5em sans-serif;
        font-weight: 700;
      }
    }

    .item2 {
      .cci {
        color: #a25a4e;
      }
      .ccc {
        color: #a25a4e;
        font: 1.5em sans-serif;
        font-weight: 700;
      }
    }

    .item3 {
      .cci {
        color: #5d7092;
      }
      .ccc {
        color: #5d7092;
        font: 1.5em sans-serif;
        font-weight: 700;
      }
    }
  }
}

.card-spheader {
  .title {
    border-left: 4px solid map-get($map: $colors, $key: "blue");
  }
}
</style>
