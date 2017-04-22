<template>
  <div class="container">
    <header class="bar bar-nav">
      <h1 class='title'>美食情报</h1>
    </header>
    <div class="bar bar-header-secondary">
      <div class="searchbar">
       <a class="searchbar-cancel">取消</a>
        <div class="search-input">
          <label class="icon icon-search" for="search"></label>
          <input type="search" id='search' placeholder='输入关键字...'/>
        </div>
      </div>
    </div>

    <div class="content list" v-infinite-scroll="loadMore">
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
    </div>
      <div class="list-block infinite-list">
<!--         <ul>
          <li class="item-content" v-for="item in items" track-by="$index">
            <div class="item-media"><i class="icon icon-dianji"></i></div>
            <div class="item-inner">
              <div class="item-title">商品名称</div>
              <div class="item-after">{{item.name}}</div>
            </div>
          </li>
        </ul> -->
      </div>
    </div>
  </div>
</template>

<script>
import VCard from '../components/Card'
import VCardItem from '../components/CardItem'
import {loader} from '../util/util'
import $ from 'zepto'

export default {
  route: {
    data ({to, next}) {
      // next()
      return this.$http.get('spy.json')
      .then(({data: {code, message, data}}) => {
        this.$set('spies', data)
        console.log(code)
      })
    }
  },
  ready () {
    for (let i = 0; i < 15; i++) {
      this.items.push({
        id: i,
        name: `demo${i + 1}`
      })
    }
    $.init()
  },
  data () {
    return {
      items: [],
      loading: false,
      spies: []
    }
  },
  computed: {
    length () {
      return this.items.length
    }
  },
  components: {
    VCard,
    VCardItem
  },
  methods: {
    loadMore () {
      if (this.loading) {
        return
      }
      this.loading = true
      let scroller = $('.list')
      loader.show()
      setTimeout(() => {
        let i = this.length
        this.items.push({
          id: i,
          name: `demo${i + 1}`
        })
        let scrollTop = scroller[0].scrollHeight - scroller.height() - 20
        scroller.scrollTop(scrollTop)
        this.loading = false
        loader.hide()
      }, 1500)

      this.$http.get('spy.json')
      .then(({data: {code, message, data}}) => {
        this.spies = this.spies.concat(data)
        console.log(this.spies.length)
      })
    }
  }
}
</script>

<style scoped>
.list-block {
  margin: .5rem 0;
}
.list {
  bottom: 2.5rem;
  padding-bot
  tom: 1rem;
}
.text {
  width: 95%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>
