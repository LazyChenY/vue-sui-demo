<template>
<div class="container">
  <header class="bar bar-nav">
  <h1 class='title'>Food Agents</h1>
</header>
  <div class="content home" distance="55" v-pull-to-refresh="refresh">
    <v-layer></v-layer>
    <slider :banner="banner"></slider>
    <bar class="home-bar">
      <bar-item path="/rank" label="排行榜" icon="preview"></bar-item>
      <bar-item path="/rank" label="我的情报" icon="dianji"></bar-item>
      <bar-item path="/collect" label="我的收藏" icon="accept"></bar-item>
    </bar>
      <v-content type="block-title" style="margin: 0 0 0.4rem;
    -webkit-box-shadow: 0 .06rem 0 #ccc;box-shadow: 0 .06rem 0 #ccc;background-color: white;">
      <btn style="float:left;margin: .4rem 0 .3rem .6rem;border:0;color:#6d6d72;padding:0">
      热门情报
      </btn>
      <btn types="link"
        style="float:right;margin: .4rem .6rem .3rem 0;border:0;border:0;padding:0"
        v-link="{path: '/tasks', replace: true}">
        更多情报
      </btn>
    </v-content>
    <div class="card-container" v-for="spy in spies">
       <v-card>
        <v-card-item
          type="header"
          valign="bottom"
          class-name="color-white no-border no-padding">
          <img class='card-cover' :src="spy.img" alt="">
        </v-card-item>
        <v-card-item type="content">
          <v-card-item type="content-inner">
            <div class="row">
              <div class="col-60">
                  <span class="color-gray">店铺名：</span><span>{{spy.name}}</span>
              </div>
              <div class="col-40">
                  <span class="color-gray">类型：</span>
                  <span style="border:1px #42b983 solid;border-radius:5px;padding:2px">{{spy.type}}</span>
              </div>
            </div>
            <span class="color-gray">地址：{{spy.adr}}</span>
            <p class="text">{{spy.text}}</p>
          </v-card-item>
        </v-card-item>
        <v-card-item type="footer">
          <a href="#" class="link">赞</a>{{spy.like}}
          <a href="#" class="link">评论</a>{{spy.comment}}
        </v-card-item>
    </v-card>


  <!-- 
      <v-card-container v-for="task in tasks | orderBy 'created' -1"
      :style="{backgroundColor: task.status === '1' ? 'white': 'rgb(224, 224, 224)' }">
        <card type="content">
          <list type="media">
              <li class="item-content">
                <item type="media">
                  <img src="http://gqianniu.alicdn.com/bao/uploaded/i4//tfscom/i3/TB10LfcHFXXXXXKXpXXXXXXXXXX_!!0-item_pic.jpg_250x250q60.jpg" width="44">
                </item>
                <item type="inner">
                  <item type="title-row">
                    <item type="text">{{task.title}}</item>
                    <item type="text">{{task.created | date 2}}</item>
                  </item>
                </item>
              </li>
          </list>
        </card>
        <card type="footer" >
          <div style="color:gray">
          赞助商：{{task.advertiser}}
          <span style="margin-left: 1rem;padding: .1rem;border: 1px solid #929292;" :style="{color: task.status === '1' ? 'green': 'gray' }">{{task.status === '0' ? '结束' : '已领'}}</span>
          </div>
          <span :style="{color: task.status === '1' ? 'orange': 'gray',fontWeight:'bold'}">{{task.read_profit}} 积分</span>
        </card>
      </v-card-container>
      -->
    </div>
  </div>
</div>
</div>
</template>

<script>
import Slider from '../components/Slider'
import Bar from '../components/Bar'
import BarItem from '../components/BarItem'
import VLayer from '../components/PullToRefreshLayer'
import VCard from '../components/Card'
import VCardItem from '../components/CardItem'
// import VSpy from '../components/Spy'
// import VCardContainer from '../components/Card'
// import Card from '../components/CardItem'
import Btn from '../components/Button'
import VContent from '../components/Content'
import List from '../components/List'
import Item from '../components/ListItem'
import $ from 'zepto'

export default {
  route: {
    data () {
      return this.$http.get('spyHot.json')
      .then(({data: {code, message, data}}) => {
        this.$set('spies', data)
        console.log(code)
      })
    }
  },
  ready () {
    $.init()
  },
  data () {
    return {
      banner: [],
      tasks: [],
      spies: []
    }
  },
  computed: {
    length () {
      return this.tasks.length
    }
  },
  methods: {
    refresh () {
      setTimeout(function () {
        let num = this.length + 1
        let title = `标题${num}`
        let adv = `abc${num}`
        let time = (new Date()).getTime() / 1000
        let point = 100 + num - 1
        this.tasks.push({
          id: num,
          title: title,
          advertiser: adv,
          status: '1',
          created: time,
          read_profit: point
        })
        $.pullToRefreshDone('.pull-to-refresh-content')
      }.bind(this), 1500)
    }
  },
  components: {
    Slider,
    Bar,
    BarItem,
    VLayer,
    // VCardContainer,
    // Card,
    VContent,
    List,
    Item,
    Btn,
    VCard,
    VCardItem
    // VSpy
  }
}
</script>

<style>
.container {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}
.home {
  /*top: -2.2rem !important;*/
}
.home-bar {
  background: #efeff4;
  height: 2.8rem;
  position: relative;
  box-shadow: 0 .01rem .05rem rgba(0,0,0,.3);
}
.home-bar .tab-item {
  height: 2.8rem;
  background-color: white;
}
.text {
  width: 95%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>
