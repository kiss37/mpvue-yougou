<template>
  <div class="container">
    <div class="search-hotspot">
      <div>
        <icon type="search"
              size="18"
              color="#bbb">
        </icon>搜索
      </div>
    </div>
    <!-- 轮播图 -->
    <swiper indicator-dots
            autoplay
            circular
            indicator-color="rgba(255, 255, 255, .3)"
            indicator-active-color="#fff">
      <block v-for="item in swiperdata"
             :key="item.goods_id">
        <swiper-item>
          <img :src="item.image_src"
               alt="">
        </swiper-item>
      </block>
    </swiper>

    <!-- 分类 -->
    <div class="categories">
      <img v-for="(item, index) in catitems"
           :key="index"
           :src="item.image_src"
           alt="">
    </div>
    <!-- 楼层区 -->
    <ul class="floor">
      <li v-for="(item, index) in floordata"
          :key="index">
        <img :src="item.floor_title.image_src"
             alt="">
        <div class="product_list">
          <img :src="item.product_list[0].image_src"
               alt="">
          <div class="right">
            <img :src="item.product_list[1].image_src"
                 alt="">
            <img :src="item.product_list[2].image_src"
                 alt="">
            <img :src="item.product_list[3].image_src"
                 alt="">
            <img :src="item.product_list[4].image_src"
                 alt="">
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 轮播图数据
      swiperdata: [],
      // 图片数据
      catitems: [],
      // 楼层区图片
      floordata: []
    }
  },
  onLoad () {
    this.getSwiperdata()
    this.getCatitems()
    this.getfloordata()
  },
  methods: {
    // 请求轮播图
    getSwiperdata () {
      this.$request({
        url: '/api/public/v1/home/swiperdata'
      }).then(data => {
        this.swiperdata = data
      })
    },
    // 请求中间图片
    getCatitems () {
      this.$request({
        url: '/api/public/v1/home/catitems'
      }).then(data => {
        this.catitems = data
      })
    },
    // 请求楼层区图片
    getfloordata () {
      this.$request({
        url: '/api/public/v1/home/floordata'
      }).then(data => {
        this.floordata = data
      })
    }
  }

}
</script>

<style lang="less">
.search-hotspot {
  height: 100rpx;
  padding: 20rpx 16rpx;
  background-color: #eb4450;
  box-sizing: border-box;
  > div {
    background-color: #fff;
    justify-content: center;
    align-items: center;
    display: flex;
    height: 60rpx;
    border-radius: 4px;
    color: #bbb;
    font-size: 16px;
    icon {
      margin: 4px 16rpx 0 0;
    }
  }
}

swiper {
  height: 340rpx;
  img {
    width: 100%;
    height: 100%;
  }
}

.categories {
  display: flex;
  height: 194rpx;
  justify-content: space-around;
  img {
    width: 128rpx;
    height: 140rpx;
  }
}
.floor {
  li {
    > img {
      width: 100%;
      height: 88rpx;
    }
  }
}
.product_list {
  padding: 20rpx 17rpx;
  display: flex;
  > img {
    width: 232rpx;
    height: 386rpx;
  }
  .right {
    flex: 1;
    font-size: 0;
    img {
      width: 232rpx;
      height: 188rpx;
      margin: 0 0 10rpx 10rpx;
    }
  }
}
</style>