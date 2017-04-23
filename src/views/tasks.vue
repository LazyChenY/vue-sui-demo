<template>
<div class="article">
  <nav class="bar bar-nav">
    <h1 class="title" v-text="title"></h1>
    <!-- <v-button types="nav link"
      class-name="pull-right"
      @click="openPanel">
      <v-icon type="more"></v-icon>
    </v-button> -->
  </nav>
  <v-tabs type="tab" class-name="article-tabs">
    <v-tab name="timer-tasks" title="限时任务" status="active"
    distance="55" v-pull-to-refresh="refreshAll">
      <v-layer></v-layer>
      <div class="myTasks">
          <v-card-container v-for="task in timerTasks | orderBy 'id' -1">
            <card type="header" class="task-title-red">{{task.title}}</card>
            <card type="content">
              <card type="content-inner">{{task.content}}
                <p class="color-gray task-time">{{task.time}}</p>
              </card>
            </card>
          </v-card-container>
      </div>
      <!-- <div class="allTasks">
          <v-card-container>
            <card type="header">card1</card>
            <card type="content">
              <card type="content-inner">
              这里是第1个card，下拉刷新会出现第2个card
              </card>
            </card>
          </v-card-container>
      </div> -->
    </v-tab>
    <v-tab name="common-tasks" title="普通任务"
    distance="55" v-pull-to-refresh="refreshMine">
      <v-layer></v-layer>
      <div class="myTasks">
          <v-card-container v-for="task in normalTasks | orderBy 'id' -1">
            <card type="header" class="task-title-blue">{{task.title}}</card>
            <card type="content">
              <card type="content-inner">{{task.content}}
                <p class="color-gray task-time">{{task.time}}</p>
              </card>
            </card>
          </v-card-container>
      </div>
    </v-tab>
  </v-tabs>
  <!-- <div class="panel-overlay"></div>
  <div class="panel panel-right panel-cover" id='panel-demo'>
    <div class="content-block">
      <p>我是从右边出现的</p>
      <p>并且我是覆盖在页面上而不是推开页面</p>
      <p></p>
      <p><button class="button close-panel">关闭</button></p>
    </div>
  </div> -->
</div>
</template>

<script>
import VButton from '../components/Button'
import VIcon from '../components/Iconfont'
import VTabs from '../components/Tabs'
import VTab from '../components/Tab'
import VLayer from '../components/PullToRefreshLayer'
import VCardContainer from '../components/Card'
import Card from '../components/CardItem'
import $ from 'zepto'

export default {
  ready () {
    $.init()
  },
  data () {
    return {
      title: '任务列表',
      normalTasks: [
        {
          id: 3,
          title: '美食情报员',
          content: '客官，今天吃了什么好吃的快给大家分享一下吧~分享之后还有高积分可以领取哦~赶快行动吧！',
          time: '2017-04-09'
        },
        {
          id: 2,
          title: '美食联络员',
          content: '刚刚不少客官发布了最新的美食情报，赶快与他们互动领取积分吧~^0^',
          time: '2017-04-09'
        },
        {
          id: 1,
          title: '美食探索员',
          content: '快去发现最近哪里有好吃又打折的分享给大家吧，分享还有积分可以领取哦~',
          time: '2017-04-09'
        }
      ],
      timerTasks: [
        {
          id: 1,
          title: '“大龙火锅”八折啦！',
          content: '即日起，进店消费满200即享受八折优惠，并另赠送菜品两份~！此次活动各大分店均有举办，吃货们快来领券哟，约起来~',
          time: '2017-04-09'
        },
        {
          id: 2,
          title: '“龙户人家”周年庆来啦！',
          content: '“龙户人家”喜迎45周年庆，凡到店消费即送特色菜品三份，每日酒水限量免费提供，更多优惠敬请到店~',
          time: '2017-04-08'
        }
      ]
    }
  },
  computed: {
    length () {
      return this.normalTasks.length
    },
    len () {
      return this.timerTasks.length
    }
  },
  methods: {
    openPanel () {
      $.openPanel('#panel-demo')
    },
    refreshAll () {
      $.showIndicator()
      setTimeout(function () {
        console.log('refreshMine')
        let num = this.len + 1
        let title = `第${num}个限时活动`
        let time = '2017-04-10'
        let content = `这里是第${num}个限时活动任务，下拉刷新会出现第${num + 1}个限时活动。`
        this.timerTasks.push({
          id: num,
          title: title,
          content: content,
          time: time
        })
        $.pullToRefreshDone('.pull-to-refresh-content')
        $.hideIndicator()
      }.bind(this), 1000)
      // $.showIndicator()
      // setTimeout(function () {
      //   console.log('refreshAll')
      //   let cardNumber = $(this.$el).find('.card').length
      //   let cardHTML = '<div class="card">' +
      //     '<div class="card-header">card' + cardNumber + '</div>' +
      //     '<div class="card-content">' +
      //     '<div class="card-content-inner">' +
      //     '这里是第' + cardNumber + '个card，下拉刷新会出现第' + (cardNumber + 1) + '个card。' +
      //     '</div>' +
      //     '</div>' +
      //     '</div>'
      //   $(this.$el).find('.allTasks').prepend(cardHTML)
      //   // 加载完毕需要重置
      //   $.pullToRefreshDone('.pull-to-refresh-content')
      //   $.hideIndicator()
      // }.bind(this), 1500)
    },
    refreshMine () {
      $.showIndicator()
      setTimeout(function () {
        console.log('refreshMine')
        let num = this.length + 1
        let title = `第${num}个普通任务`
        let time = '2017-04-11'
        let content = `这里是第${num}个普通任务，下拉刷新会出现第${num + 1}个card。`
        this.normalTasks.push({
          id: num,
          title: title,
          content: content,
          time: time
        })
        $.pullToRefreshDone('.pull-to-refresh-content')
        $.hideIndicator()
      }.bind(this), 1000)
    }
  },
  components: {
    VButton,
    VIcon,
    VTabs,
    VTab,
    VLayer,
    VCardContainer,
    Card
  }
}
</script>

<style>
.article {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}
.article-tabs .buttons-tab {
  z-index: 10;
  margin-top:2.2rem;
}
#common-tasks, #timer-tasks {
  top: 2rem;
}
.task-title-red {
  color: #ee6e73;
  font-weight: 600;
}
.task-title-blue {
  color: #0894ec;
  font-weight: 600;
}
.task-time {
  padding-left: 12rem;
}
</style>
