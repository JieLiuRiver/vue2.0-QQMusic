<template>
    <div class="search-wrapper" :style="{'height': screenHeight}">
      <div class="bar">
          <div class="input-wrapper f-pr">
            <input type="search" @focus="getFocus" v-model="searchModel" @keyup="writingContent" class="search-input" name="" autocomplete="off" placeholder="搜索歌曲、歌单、专辑">
            <span class="icon icon-search f-pa f-ib"></span>
            <span class="del-btn f-pa f-ib" v-show="isNeedToDel" @click.stop="clearInputValue"></span>
          </div>
          <div class="cancle-btn" v-show="isShowCancleBtn" @click="hideBtn">取消</div>
      </div>
      <div class="hot-key-wrapper" v-show="!isShowCancleBtn">
        <h3 class="title">热门搜索</h3>
        <div class="tag-w">
          <a href="javascript:;" class="tag f-ib" v-for="(item, index) in keyWordTagData" :class="{'hot':index == 0}">
              {{item.text}}
          </a>
        </div>
      </div>
    </div>
</template>
<script>
  export default{
    name: '',
    props: {},
    data() {
      return {
        screenHeight: screen.height + 'px',
        isShowCancleBtn: false,
        isNeedToDel: false,
        searchModel: '',
        keyWordTagData: this.$store.state.pageData.keyWordTagData
      }
    },
    methods: {
      getFocus() {
        this.isShowCancleBtn = true
      },
      hideBtn() {
        this.isShowCancleBtn = false
      },
      writingContent() {
        if (this.searchModel != '') {
          this.isNeedToDel = true
        } else {
          this.isNeedToDel = false
        }
      },
      clearInputValue() {
        this.searchModel = ''
        this.isNeedToDel = false
      }
    }
  };
</script>
<style scoped lang="stylus" rel="stylesheet/stylus">
  @import '../../common/css/computed.styl';

  .search-wrapper
    background: #fff
    r1(font-size, 15)
    .bar
      r1(padding, 10)
      background: #f4f4f4
      display: -webkit-box
      display: box
      -webkit-box-orient: horizontal
      -webkit-box-align: center
      box-orient: horizontal
      box-align: center
      .input-wrapper
        background: #fff
        r1(border-radius, 3)
        r2(padding-top, 8, padding-bottom, 8)
        r2(padding-left,35, padding-right,12)
        box-flex: 1
        -webkit-box-flex: 1
        .search-input
          r2(height, 20, line-height, 20)
          width: 100%
          color: rgba(0,0,0,.3)
          border: none
          r1(font-size, 14)
          -webkit-appearance: textfield
          appearance: textfield
        .icon-search
          r2(width, 18, height, 18)
          r2(left,10, top, 9)
          background: url(../../common/images/search.png)
          background-repeat: no-repeat
          background-size: cover
        .del-btn
          r2(width, 18, height, 18)
          r1(border-radius, 9)
          r2(top, 9, right, 12)
          background: #b1b1b1 url(../../common/images/close.png)
          background-repeat: no-repeat
          background-size: cover
      .cancle-btn
        r2(height, 36, line-height,36)
        r1(font-size, 14)
        r2(padding-left, 10, padding-right, 10)
    .hot-key-wrapper
      r2(padding-left, 15, padding-right, 15)
      r2(padding-top, 15, padding-bottom, 10)
      .title
        color: rgba(0,0,0,.6)
        r1(margin-bottom, 8)
        font-weight: bold
        r1(font-size, 14)
      .tag-w
        .tag
          r1(font-size, 14)
          r2(padding-left, 10, padding-right, 10)
          r2(margin-right, 14, margin-bottom, 10)
          r1(border-radius, 99)
          border: 1px solid rgba(0,0,0,.6)
          word-break: break-all
          r2(line-height, 36, height, 36)
        .hot
          color: #fc4524
          border-color: #fc4524
</style>
