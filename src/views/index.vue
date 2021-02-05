<template>
  <div class="index">
    <div class="container">
      <div class="swiper-box">
        <div class="nav-menu">
          <ul class="menu-wrap" v-for="(kind,i) in cateList" :key="i">
            <li class="menu-item">
              <a href="javascript:;">{{kind.name}}</a>
              <div class="children">
                <ul v-for="(item,i) in kind.menuList" :key="i">
                  <li v-for="(sub,j) in item" :key="j">
                    <a :href="sub?'/#/product/'+sub.good_id:''">
                      <img :src="sub?sub.icon:''">
                      {{sub?sub.name:''}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
<!--            <li class="menu-item">-->
<!--              <a href="javascript:;">超划算套餐</a>-->
<!--            </li>-->

          </ul>
        </div>

        <!--        变换图-->
        <swiper :options="swiperOption">
          <swiper-slide v-for="(item,index) in slideList" :key="index">
            <a :href="'/#/product/'+item.id"><img :src="item.img"></a>
          </swiper-slide>
          <!-- Optional controls -->
          <div class="swiper-pagination"  slot="pagination"></div>
          <div class="swiper-button-prev" slot="button-prev"></div>
          <div class="swiper-button-next" slot="button-next"></div>
        </swiper>
      </div>

      <!--        变换图下的四个小图-->
      <div class="ads-box">
        <a :href="'/#/product/'+item.id" v-for="(item,index) in adsList" :key="index">
          <img v-lazy="item.img">
        </a>
      </div>

      <!--      横幅广告-->
    </div>


    <div class="banner">
      <a href="/#/product/30">
        <img src="/imgs/banner/1.webp">

      </a>
    </div>
    <div class="product-box">
      <div class="container">
        <h2>手机</h2>
        <div class="wrapper">
          <!--          左下角长短高长图-->
          <div class="banner-left">
            <a href="/#/product/7"><img v-lazy="'/imgs/leftbottompic/mix-alpha.jpg'"></a>
          </div>
          <div class="list-box">
            <div class="list" v-for="(arr,i) in phoneList" :key="i">
              <div class="item" v-for="(item,j) in arr" :key="j">

                <!--                新品绿色标志-->
                <span :class="{'new-pro':j%2==0}">新品</span>
                <div class="item-img">
                  <img v-lazy="item.imageFoot">
                </div>

                <!--                名字子标题价格-->
                <div class="item-info">
                  <h3>{{item.name}}</h3>
                  <p>{{item.subtitle}}</p>
                  <p class="price" @click="addCart(item.good_id)">{{item.price}}元</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="banner">
      <a href="/#/product/30">
        <img :src="'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/41d16e66381cfeda7b6b39ab67678d5e.jpg?thumb=1&w=1226&h=120&f=webp&q=90'">

      </a>
    </div>

    <div class="product-box">
      <div class="container">
        <h2>电视</h2>
        <div class="wrapper">
          <!--          左下角长短高长图-->
          <div class="banner-left">
            <a href="/#/product/7"><img v-lazy="'/imgs/leftbottompic/2.webp'"></a>
          </div>
          <div class="list-box">
            <div class="list" v-for="(arr,i) in TVList" :key="i">
              <div class="item" v-for="(item,j) in arr" :key="j">

                <!--                新品绿色标志-->
                <span :class="{'new-pro':j%2==0}">新品</span>
                <div class="item-img">
                  <img v-lazy="item.imageFoot">
                </div>

                <!--                名字子标题价格-->
                <div class="item-info">
                  <h3>{{item.name}}</h3>
                  <p>{{item.subtitle}}</p>
                  <p class="price" @click="addCart(item.good_id)">{{item.price}}元</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>


    <div class="banner">
      <a href="/#/product/30">
        <img :src="'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/9880db34d227b6c1df5b45cb7df4f465.jpg?thumb=1&w=1226&h=120&f=webp&q=90'">
      </a>
    </div>

    <div class="product-box">
      <div class="container">
        <h2>周边</h2>
        <div class="wrapper">
          <!--          左下角长短高长图-->
          <div class="banner-left">
            <a href="/#/product/7"><img v-lazy="'/imgs/leftbottompic/1.jpg'"></a>
          </div>
          <div class="list-box">
            <div class="list" v-for="(arr,i) in otherList" :key="i">
              <div class="item" v-for="(item,j) in arr" :key="j">

                <!--                新品绿色标志-->
                <span :class="{'new-pro':j%2==0}">新品</span>
                <div class="item-img">
                  <img v-lazy="item.imageFoot">
                </div>

                <!--                名字子标题价格-->
                <div class="item-info">
                  <h3>{{item.name}}</h3>
                  <p>{{item.subtitle}}</p>
                  <p class="price" @click="addCart(item.good_id)">{{item.price}}元</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!--    预约维修服务,7天无理由退货-->
    <ServiceBar></ServiceBar>

    <Modal
      title="提示"
      sureText="查看购物车"
      cancelText="取消"
      btnType="3"
      modalType="middle"
      :showModal="showModal"
      @submit="goToCart"
      @cancel="showModal=false">
      <template v-slot:body>
        <p>商品添加成功！</p>
      </template>
    </Modal>
  </div>
</template>
<script>
import ServiceBar from './../components/ServiceBar'
import Modal from './../components/Modal'
import { swiper, swiperSlide } from 'vue-awesome-swiper'
import 'swiper/dist/css/swiper.css'
export default {
  name: 'index',
  components: {
    swiper,
    swiperSlide,
    ServiceBar,
    Modal
  },
  data () {
    return {
      swiperOption: {
        autoplay: true,
        loop: true,
        effect: 'cube',
        cubeEffect: {
          shadowOffset: 100,
          shadowScale: 0.6
        },
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      },

      //变换图
      slideList: [
        {
          id: '1',
          img: '/imgs/slider/slide-1.jpg'
        },
        {
          id: '3',
          img: '/imgs/slider/lunbo1.webp'
        },
        {
          id: '17',
          img: '/imgs/slider/lunbo2.webp'
        },
        {
          id: '40',
          img: '/imgs/slider/lunbo3.webp'
        },
        {
          id: '40',
          img: '/imgs/slider/slide-4.jpg'
        }
      ],

      cateList:[
        {
          categoryId: '',
          name: '',
          menuList: [
            // 6行4列的二维数组
            [
              {
                good_id: 1,
                icon: '/imgs/item-box-1.png',
                name: '小米CC9'
              },
              {
                good_id: 2,
                icon: '/imgs/item-box-2.png',
                name: '小米8青春版'
              },
              {
                good_id: 3,
                icon: '/imgs/item-box-3.jpg',
                name: 'Redmi K20 Pro'
              },
              {
                good_id: 4,
                icon: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/a51c1afa4db8e47e62fad1f6fa4a8970.png?thumb=1&w=40&h=40&f=webp&q=90',
                name: '小米11'
              }
            ],
            [
              {
                good_id: 5,
                icon: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/461bf013d08a7a91423cafcbc5ff9339.jpg?thumb=1&w=40&h=40&f=webp&q=90',
                name: 'Redmi K30 Pro 变焦版'
              },
              {
                good_id: 6,
                icon: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/76378ce289a36fcfa29f704ba90b4155.png?thumb=1&w=40&h=40&f=webp&q=90',
                name: 'Redmi Note 9 5G'
              },
              {
                good_id: 7,
                icon: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/0cadc8b00dbe3b5615bd6ab657715baf.png?thumb=1&w=40&h=40&f=webp&q=90',
                name: 'Redmi 9'
              },
              {
                good_id: 8,
                icon: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/5ca871528d3420622f21f25be7aba58c.png?thumb=1&w=40&h=40&f=webp&q=90',
                name: '小米10至尊纪念版'
              }
            ],
            [
              {
                id: 9,
                img: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/7a98170e97ca5df8f5ad2470a8a2d01e.jpg?thumb=1&w=40&h=40&f=webp&q=90',
                name: 'Redmi K30 5G'
              },
              {
                id: 10,
                img: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/970c6b287eb89620f5ee8e2b347f6f3d.png?thumb=1&w=40&h=40&f=webp&q=90',
                name: 'Redmi Note 9 Pro 5G'
              },
              {
                id: 11,
                img: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/1db88cd66ff1a6a3e75116988b7f3e12.jpg?thumb=1&w=40&h=40&f=webp&q=90',
                name: 'Redmi 9A'
              },
              {
                id: 12,
                img: 'https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/4a7a4f24061860901f724b6ba6d75fd9.png?thumb=1&w=40&h=40&f=webp&q=90',
                name: '小米10'
              }
            ]
          ]
        },
        {
          cateid: '',
          catename: '',
          menuList: [
              [{},{},{},{},{},{}],
            [],
            [],
            []
          ]
        }
      ]
      ,
      adsList: [
        {
          id: 2,
          img: '/imgs/ads/ads-1.png'
        }, {
          id: 3,
          img: '/imgs/ads/ads-2.jpg'
        }, {
          id: 6,
          img: '/imgs/ads/ads-3.png'
        }, {
          id: 5,
          img: '/imgs/ads/lunboxia1.jpg'
        }
      ],
      phoneList: [],
      TVList:[],
      otherList:[],
      showModal: false
    }
  },
  mounted () {
    this.init()
  },
  methods: {
    init () {

      this.axios.get('http://localhost:8080/index/category',

      ).then((res) => {
        this.cateList=res.data.cateList
      })

      this.axios.get('http://localhost:8080/index/productfoot', {
        params: {
          categoryId: 1,
          pageStart: 1
        }
      }).then((res) => {
        // res.list = res.list.slice(6, 14)
        this.phoneList = [res.data.slice(0, 4), res.data.slice(4, 8)]
        // this.phoneList=res.data
      })

      this.axios.get('http://localhost:8080/index/productfoot', {
        params: {
          categoryId: 2,
          pageStart: 1
        }
      }).then((res) => {
        // res.list = res.list.slice(6, 14)
        // this.phoneList = [res.list.slice(0, 4), res.list.slice(4, 8)]
        this.TVList=[res.data.slice(0, 4), res.data.slice(4, 8)]
      })

      this.axios.get('http://localhost:8080/index/productfoot', {
        params: {
          categoryId: 8,
          pageStart: 1
        }
      }).then((res) => {
        // res.list = res.list.slice(6, 14)
        // this.phoneList = [res.list.slice(0, 4), res.list.slice(4, 8)]
        this.otherList=[res.data.slice(0, 4), res.data.slice(4, 8)]
      })

    },
    addCart (id) {
      let token
      if(sessionStorage.getItem("token")){
        token=sessionStorage.getItem("token")
      }
      else {
        token='null'
      }
      let username= sessionStorage.getItem("username")
      this.axios.post('http://localhost:8080/carts/push', {
        token:token.replace(/^\"|\"$/g,''),
        productId: id,
        username: username,
        select: true

      }).then((res) => {
        this.showModal = true
        this.$store.dispatch('saveCartCount', res.cartTotalQuantity)
      })
    },
    goToCart () {
      this.$router.push('/cart')
    }
  }
}
</script>
<style lang="scss">
  @import './../assets/scss/config.scss';
  @import './../assets/scss/mixin.scss';
  .index{
    .swiper-box{
      .nav-menu{
        position:absolute;
        width:264px;
        height:451px;
        z-index:5;
        padding:26px 0;
        // 带透明度的背景色
        background-color:#55585a7a;
        box-sizing:border-box;
        .menu-wrap{
          .menu-item{
            height:50px;
            line-height:50px;
            a{
              position:relative;
              display:block;
              font-size:16px;
              color:#ffffff;
              padding-left:30px;
              &:after{
                position:absolute;
                right:30px;
                top:17.5px;
                content:' ';
                @include bgImg(10px,15px,'/imgs/icon-arrow.png');
              }
            }
            &:hover{
              background-color:$colorA;
              .children{
                display:block;
              }
            }
            .children{
              display:none;
              width:962px;
              height:451px;
              background-color:$colorG;
              position:absolute;
              top:0;
              left:264px;
              border:1px solid $colorH;
              ul{
                display:flex;
                justify-content:space-between;
                height:75px;
                li{
                  height:75px;
                  line-height:75px;
                  flex:1;
                  padding-left:23px;
                  a{
                    color:$colorB;
                    font-size:14px;
                    img{
                      width:42px;
                      height:35px;
                      vertical-align:middle;
                      margin-right:15px;
                    }
                  }
                }
              }
            }
          }
        }
      }
      .swiper-container {
        height: 451px;
        .swiper-button-prev{
          left:274px;
        }
        img{
          width:100%;
          height:100%;
        }
      }
    }
    .ads-box{
      @include flex();
      margin-top:14px;
      margin-bottom:31px;
      a{
        width:296px;
        height:167px;
        // img{  base.scss写过了
        //   width:100%;
        //   height:100%;
        // }
      }
    }
    .banner{
      margin-bottom:50px;
    }
    .product-box{
      background-color:$colorJ;
      padding:30px 0 50px;
      h2{
        font-size:$fontF;
        height:21px;
        line-height:21px;
        color:$colorB;
        margin-bottom:20px;
      }
      .wrapper{
        display:flex;
        .banner-left{
          margin-right:16px;
          img{
            width:224px;
            height:619px;
          }
        }
        .list-box{
          .list{
            @include flex();
            width:986px;
            margin-bottom:14px;
            &:last-child{
              margin-bottom:0;
            }
            .item{
              width:236px;
              height:302px;
              background-color:$colorG;
              text-align:center;
              span{
                display:inline-block;
                width:67px;
                height:24px;
                font-size:14px;
                line-height:24px;
                color:$colorG;
                &.new-pro{
                  background-color:#7ECF68;
                }
                &.kill-pro{
                  background-color:#E82626;
                }
              }
              .item-img{
                img{
                  width:100%;
                  height:195px;
                }
              }
              .item-info{
                h3{
                  font-size:14px;
                  color:$colorB;
                  line-height:14px;
                  font-weight:bold;
                }
                p{
                  color:$colorD;
                  line-height:13px;
                  margin:6px auto 13px;
                }
                .price{
                  color:#F20A0A;
                  font-size:$fontJ;
                  font-weight:bold;
                  cursor:pointer;
                  &:after{
                    @include bgImg(22px,22px,'/imgs/icon-cart-hover.png');
                    content:' ';
                    margin-left:5px;
                    vertical-align: middle;
                  }
                }
              }
            }
          }
        }
      }
    }
  }
</style>
