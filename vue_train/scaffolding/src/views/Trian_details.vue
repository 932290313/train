<template>
  <div class="detail">
    <!-- 车票查询头部 -->
    <mt-header title="火车票订单">
      <router-link to="/person" slot="left">
        <mt-button icon="back"></mt-button>
      </router-link>
    </mt-header>
    <!-- 车票查询头部结尾 -->
    <!-- 车票开始 -->
    <div class="container">
      <div>
        <span>我的订单</span>
        <span>刷新</span>
      </div>
      <div class="route">
        <span>北京 -> 上海 - D1997</span>
        <span>未进站</span>
      </div>
      <div class="route">
        <span>{{this.moment.unix(this.travel_timestar).format('MMMM/Do/YYYY, h:mm a')}}开</span>
        <span>¥248</span>
      </div>
      <div class="route">
        <span>到达{{this.travel_timeover}}</span>
      </div>
      <div class="route">
        <span>购票时间{{this.buying_time}}</span>
      </div>
      <div class="route">
        <span>乘车人：xxx</span>
      </div>
    </div>
    <div class="change">
      <mt-button size="large" type="primary">修改订单</mt-button>
    </div>
    <!-- 车票结束 -->
  </div>
</template>

<style scoped>
.container > div:first-child > span:last-child {
  color: #26a2ff;
}
.change {
  margin: 0.1rem;
}
.container {
  padding: 0.5rem;
  margin-top: 0.3rem;
}
.container > div {
  display: flex;
  justify-content: space-between;
  padding: 0.25rem;
}
.container > .route {
  background: #fff;
  border-radius: 0.25rem;
  padding: .3rem 0.5rem;
}
.detail {
  background: #f9f9f9;
  padding-bottom: 36.5rem;
}
</style>

<script>
export default {
  data() {
    return {
      travel_timestar:"",
      buying_time:"",
      travel_timeover:"",
    };
  },
  methods: {

  },
   mounted() {
    // 获取文章分类信息
    this.axios.get("/ticket_details?ticket_uid=" + this.$store.state.uid).then((result) => {
      console.log(result.data);
      //this.a = result.data;
      let results=result.data[0];
      this.travel_timestar=results.travel_timestar;
      this.buying_time=results.buying_time;
      this.travel_timeover=results.travel_timeover;
    });
    // 获取默认文章分类下的文章数据
    //this.load(this.active,this.page)
  },
};
</script>