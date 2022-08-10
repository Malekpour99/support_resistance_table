<template lang="pug">
.total-container
  .data-row
    .head-title
      | نماد
    .head-title(@click="general_sorter('dis_support')")
      | فاصله تا حمایت
    .head-title
      | محدوده حمایت
    .head-title(@click="general_sorter('dis_resistance')")
      | فاصله تا مقاومت
    .head-title
      | محدوده مقاومت
    .head-title(@click="general_sorter('avg_buyer_power_10day')")
      | میانگین قدرت خریدار 10 روزه
    .head-title(@click="general_sorter('buyer_power_to_10dayAvg')")
      | قدرت خریدار فعلی به میانگین 10 روزه
    .head-title(@click="general_sorter('buyer_power_to_marketAvg')")
      | نسبت قدرت خریدار فعلی به میانگین بازار
    .head-title(@click="general_sorter('buyer_power_diff')")
      | تغییرات قدرت خریدار از اول صبح
    .head-title(@click="general_sorter('cash_flow_10day')")
      | جریان نقدینگی حقیقی 10 روزه
    .head-title(@click="general_sorter('yesterday_volume_co')")
      | ضریب حجمی دیروز
    .head-title(@click="general_sorter('volume_index')")
      | شاخص حجمی
  .data-row(v-for="(item, index) in shareInfo", :key="index")
    .main-data
      | {{ item.tse_symbol }}
    .main-data
      | %{{ item.dis_support }} ({{ item.support }})
    .main-data
      | {{ item.support_top }} | {{ item.support_botton }}
    .main-data
      | %{{ item.dis_resistance }} ({{ item.resistance }})
    .main-data
      | {{ item.resistance_top }} | {{ item.resistance_botton }}
    .main-data
      | {{ item.avg_buyer_power_10day }}
    .main-data
      | {{ item.buyer_power_to_10dayAvg }}
    .main-data
      | {{ item.buyer_power_to_marketAvg }}
    .main-data
      | {{ item.buyer_power_diff }}
    .main-data
      | {{ item.cash_flow_10day }}
    .main-data
      | {{ item.yesterday_volume_co }}
    .main-data
      | {{ item.volume_index }}
</template>

<script>
export default {
  name: "DataChart",
  props: {
    AverageInfo: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      shareInfo: [],
      ascending: true,
      decending: false,
    };
  },
  computed: {},
  methods: {
    symbol_sorter() {
      if (this.ascending == true) {
        this.shareInfo.sort((a, b) =>
          ("" + a.tse_symbol).localeCompare(b.tse_symbol)
        );
        this.ascending = false;
      } else {
        this.shareInfo.sort((a, b) =>
          ("" + b.tse_symbol).localeCompare(a.tse_symbol)
        );
        this.ascending = true;
      }
    },
    general_sorter(criteria) {
      if (this.ascending == true) {
        this.shareInfo.sort((a, b) => {
          return (
            (a = parseFloat(a[criteria])), (b = parseFloat(b[criteria])), a - b
          );
        });
        this.ascending = false;
      } else {
        this.shareInfo.sort((a, b) => {
          return (
            (a = parseFloat(a[criteria])), (b = parseFloat(b[criteria])), b - a
          );
        });
        this.ascending = true;
      }
    },
  },
  created() {
    this.shareInfo = this.AverageInfo
  }
};
</script>

<style scoped>
.total-container {
  max-width: 1440px;
  margin: 0 auto;
}
.data-row {
  display: flex;
  justify-content: space-between;
  flex-wrap: nowrap;
  direction: rtl;
}
.head-title {
  font-family: "B Yekan";
  font-size: 14px;
  text-align: center;
  background: #61626a;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 7.2%;
  min-height: 5rem;
  margin: 0.12em;
  padding: 0.3em;
  border-radius: 5px;
  overflow: auto;
  scrollbar-width: thin;
}
.head-title:hover {
  background: #cea71d;
  cursor: pointer;
}
.main-data {
  font-family: "B Yekan";
  font-size: 14px;
  background: #444753;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 7.2%;
  min-height: 5rem;
  margin: 0.12em;
  padding: 0.3em;
  border-radius: 5px;
  overflow: auto;
  scrollbar-width: thin;
  cursor: default;
}
</style>
