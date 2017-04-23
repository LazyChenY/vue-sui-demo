<template>
<div class="content feedback">
  <header class="bar bar-nav">
    <a class="button button-link button-nav pull-left" v-link="{path: '/more', replace: true}">
    <span class="icon icon-left"></span>
    </a>
    <h1 class="title" v-text="title"></h1>
  </header>
<!--<div class="row sub-title">
    欢迎每一位用户提出留言与建议
  </div> -->
  <div class="content-block">
    <div class="feedback-label">
      <span style="color:red"></span> 情报正文：
    </div>
    <div class="item-input">
      <textarea rows="7" placeholder="请输入美食情报正文，不少于五个字哦~"></textarea>
    </div>
    <div class="feedback-label">
      指引其它小吃货们找到美食吧！
    </div>
    <div class="feedback-input">
      <input type="text" placeholder="店铺名">
      <input type="text" placeholder="地址">
      <input type="text" placeholder="美食类型" id='picker'/>
    </div>
    <p><a href="#" class="button button-round pic">添加图片</a></p>
  </div>
  <div class="submit-button">
    <button class="button button-big button-fill">提交</button>
  </div>
</div>
</template>

<script>
import $ from 'zepto'

export default {
  ready () {
    $.init()
    $('#picker').picker({
      // toolbarTemplate: '<header class="bar bar-nav"><button class="button button-link pull-left">按钮</button><button class="button button-link pull-right close-picker">确定</button><h1 class="title">标题</h1></header>',
      cols: [
        {
          textAlign: 'center',
          values: ['火锅', '串串', '烧烤', '干锅', '海鲜', '中餐', '西餐']
        }
      ]
    })
  },
  data () {
    return {
      title: '发布情报'
    }
  }
}
</script>

<style>
.sub-title {
  margin-top: 2.2rem;
  background-color: white;
  height: 2.2rem;
  font-size: .8rem;
  font-weight: normal;
  line-height: 2.2rem;
  text-align: center;
  border-bottom: 1px solid #d8d8d9;
}
.feedback .content-block {
  margin: 2.3rem 0 0 0;
  padding: 0 .45rem;
}
.feedback-label {
  font-size: .7rem;
  line-height: 1.2rem;
}
.feedback-input input{
  width: 100%;
  height: 2.15rem;
  font-size: .7rem;
  padding: .4rem .5rem;
  background-color: #fff;
  margin-bottom: .3rem;
  border: 1px solid rgba(0,0,0,.2);
  border-radius: .2rem;
}
.feedback textarea {
  height: auto;
  resize: none;
  width: 100%;
  font-size: .7rem;
  -webkit-appearance: none;
  padding: .4rem .5rem;
  -webkit-user-select: text;
  background-color: #fff;
  border: 1px solid rgba(0,0,0,.2);
  border-radius: .2rem;
  outline: 0;
}
.feedback .submit-button {
  margin-top: .8rem;
  width: 100%;
  padding: 0 .45rem;
}
.feedback .submit-button button {
  background-color: #0894ec;
  width: 100%;
  line-height: 2.1rem !important;
  height: 2.1rem !important;
}
.pic {
  color: gray;
  border: 1px solid gray;
}
</style>