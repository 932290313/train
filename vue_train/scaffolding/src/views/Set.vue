<template>
  <div class="set">
    <mt-header title="设置">
      <router-link to="/person" slot="left">
        <mt-button icon="back"></mt-button>
      </router-link>
    </mt-header>
    <div class="safe">
      <p>安全设置</p>
      <span>></span>
    </div>
    <div class="about" v-for="(v, i) of 7" :key="i">
        <!--  v-for="(v, i) of 7" :key="i" -->
      <div>
        <p>关于高铁管家</p>
        <span>></span>
      </div>
    </div>
  </div>
</template>>

<style scoped>
.set {
  background: #f0eeee;
  height: 100rem;
  padding: 0.5rem;
}
.set > .safe,.set>.about {
  display: flex;
  justify-content: space-between;
  background: #fff;
  border-radius: .2rem;
}
.set>.safe{
  margin: 0.5rem 0;
  padding: 0.5rem;
}
.set>.about>div{
    border-bottom: .1rem solid #fefefe;
    display: flex;
    padding: .8rem 0 .8rem .5rem;
}
.set>.about>div>span{
    margin-left: 14.65rem;
}
.mint-header {
  background: #ffffff;
  color: #333;
}
</style>