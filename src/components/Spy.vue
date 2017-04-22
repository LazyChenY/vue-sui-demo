<template>
  <div class="spy" v-for="spy in spies">
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
              <div class="col-33">
                  <span class="color-gray">店铺名：{{spy.name}}</span>
              </div>
              <div class="col-33">
                  <span class="color-gray">地址：{{spy.adr}}</span>
              </div>
              <div class="col-33">
                  <span class="color-gray">类型：{{spy.type}}</span>
              </div>
            </div>
            <p>{{spy.text}}</p>
          </v-card-item>
        </v-card-item>
        <v-card-item type="footer">
          <a href="#" class="link">赞</a>{{spy.like}}
          <a href="#" class="link">评论</a>{{spy.comment}}
        </v-card-item>
    </v-card>
  </div>
</template>

<script>
  import VCard from './Card'
  import VCardItem from './CardItem'

  export default {
    // route: {
    //   data () {
    //     return this.$http.get('spy.json')
    //     .then(({data: {code, message, data}}) => {
    //       this.$set('spies', data)
    //       console.log(code)
    //     })
    //   }
    // },
    route: {
      data () {
        return this.$http.get('tasks.json')
        .then(({data: {code, message, data}}) => {
          this.$set('spies', data)
          console.log(code)
        })
      }
    },
    data () {
      return {
        spies: []
      }
    },
    components: {
      VCard,
      VCardItem
    }
  }
</script>
<style>
  .spy {
 /* position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;*/
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}
</style>