<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <tab-control :titles="['流行','新款','精选']"
                @tabClick="tabClick"
                ref="tabControl1"
                class="tab-control"
                v-show="isTabFixed"></tab-control>
    <scroll class="content" 
            ref="scroll" 
            :probe-type="3" 
            @scroll="contentScroll"
            :pull-up-load="true"
            @pullingUp="loadMore">
      <home-swiper :banners="banners" @swiperImageLoad="swiperImageLoad"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control :titles="['流行','新款','精选']"
                  @tabClick="tabClick"
                  ref="tabControl2"></tab-control>
      <goods-list :goods="showGoods"></goods-list>
    </scroll>
    
    <back-top @click.native="backClick" v-show="isshowBackTop"/>
  </div>
</template>

<script>
  import NavBar from "@/components/common/navbar/NavBar.vue"
  import TabControl from "@/components/content/tabControl/TabControl.vue"
  import GoodsList from "@/components/content/goods/GoodsList.vue"
  import Scroll from "@/components/common/scroll/Scroll.vue"
  import BackTop from "@/components/content/backTop/BackTop.vue"
  
  import HomeSwiper from "./childComps/HomeSwiper.vue"
  import RecommendView from "./childComps/RecommendView.vue"
  import FeatureView from "./childComps/FeatureView.vue"
  
  import { 
    getHomeMultidata,
    getHomeGoods } from "@/network/home"
  import emitter from "@/eventbus"
  import {debounce} from "@/common/utils"



export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    GoodsList,
    Scroll,
    BackTop,
    HomeSwiper,
    RecommendView,
    FeatureView,
    Scroll
},
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0, list: []},
      },
      currentType: 'pop',
      isshowBackTop: false,
      tabOffsetTop: 0,
      isTabFixed: false,
      saveY: 0
    }
  },
  computed: {
    showGoods(){
      return this.goods[this.currentType].list
    },
    activated() {
      this.$refs.scroll.refresh()
      this.$refs.scroll.scrollTo(0, this.saveY, 0)
    },
    deactivated() {
      this.saveY = this.$refs.scroll.getScrollY()
    }
  },
  created() {
    // 请求多个数据
    this.getHomeMultidata()
    // 请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')

  },
  mounted() {
    // 监听图片加载完成
    const refresh = debounce(this.$refs.scroll.refresh,200)
    emitter.on("itemImageLoad",() => {
      refresh()
    })
  }
  ,
  methods: {
    tabClick(index){
      switch (index) {
        case 0 :
          this.currentType = 'pop'
          break
        case 1 :
          this.currentType = 'new'
          break
        case 2 :
          this.currentType = 'sell'
          break
      }
      this.$refs.tabControl1.currentType = index
      this.$refs.tabControl2.currentType = index
      this.$refs.tabControl1.currentType = this.$refs.tabControl2.currentType
      this.$refs.tabControl2.currentType = this.$refs.tabControl1.currentType
      
    },
    getHomeMultidata(){
      getHomeMultidata().then(res => {
      // this.result = res;
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res =>{
        this.goods[type].list.push(...res.data.list),
        this.goods[type].page += 1

        // 完成加载
        this.$refs.scroll.finishPullUp()
      }
    )
    },
    backClick(){
      this.$refs.scroll.scrollTo(0,0)
    },
    contentScroll(position){
      // 判断是否显示滑到顶部
      this.isshowBackTop = (-position.y) > 1000
      // 判断是否显示tab-control
      this.isTabFixed = (-position.y) > this.tabOffsetTop
    },
    loadMore(){
      this.getHomeGoods(this.currentType)
    },
    swiperImageLoad(){
      // 获取tabControl的offsetTop
      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop
    }
  },
}
</script>

<style scoped>
  #home {
    position: relative;
    height: 100vh;
  }
  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
  }
  .content {
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
  .tab-control {
    position: relative;
    z-index: 9;
  }
</style>