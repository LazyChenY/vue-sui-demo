<template>
  <div class="container">
    <header class="bar bar-nav">
    	<a class="button button-link button-nav pull-left" v-link="{path: '/tasks', replace: true}">
    		<span class="icon icon-left"></span>
    	</a>
      <h1 class='title'>我的情报</h1>
    </header>
    <div class="content list" v-infinite-scroll="loadMore">
    <!-- <div class="card-container" v-for="spy in spies"> -->
    <div class="card-container">
       <v-card>
        <v-card-item
          type="header"
          valign="bottom"
          class-name="color-white no-border no-padding">
          <!-- <img class='card-cover' :src="spy.img" alt=""> -->
          <img class='card-cover' src="../../static/img/qb01.jpg" alt="">
        </v-card-item>
        <v-card-item type="content">
          <v-card-item type="content-inner">
            <div class="row">
              <div class="col-60">
                  <span class="color-gray">店铺名：</span><span>{{spyName}}</span>
              </div>
              <div class="col-40">
                  <span class="color-gray">类型：</span>
                  <span style="border:1px #42b983 solid;border-radius:5px;padding:2px">{{spyType}}</span>
              </div>
            </div>
            <span class="color-gray">地址：{{spyAdr}}</span>
            <p class="text">{{spyText}}</p>
          </v-card-item>
        </v-card-item>
        <v-card-item type="footer">
          <a href="#" class="link">赞</a>
          <a href="#" class="link">评论</a>
        </v-card-item>
    </v-card>
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
    $.init()
    for (let i = 0; i < 15; i++) {
      this.items.push({
        id: i,
        name: `demo${i + 1}`
      })
    }
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
  props: ['spyName', 'spyText', 'spyAdr', 'spyType'],
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
.search {
  background-color: rgba(0,0,0,0.1);
}
.search-input {
  background-color: #fff;
  border-radius: 3px;
  margin: 5px 8px;
}
#search {
  outline: none;
  border: none;
  height: 18px;
}
.container {
	/*position: relative;*/
	/*top: 500px;*/
	display: none;
}
</style>
