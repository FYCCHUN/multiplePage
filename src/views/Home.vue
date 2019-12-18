<template>
  <div class="home">
    <button @click='share()'>app 内分享</button>
    <div class='wrap' style='margin-top: 20px;' v-if='showCard'>
        <a @click='openSharePage("facebook")' style='margin-right: 10px' >facebook</a>
        <a @click='openSharePage("twitter")' style='margin-right: 10px'>twitter</a>
        <a @click='openSharePage("facebook")' style='margin-right: 10px'>ins</a>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'home',
  data(){
    return {
      showCard: false,
      title: 'Truck path app share.',
      href: 'https://www.baidu.com'
    }
  },
  components: {
  },
  methods: {
    openSharePage(type) {
      const toOpen = function(url) {
        const option =
          'toolbar=yes, location=yes, directories=no, status=no, menubar=yes, scrollbars=yes, resizable=no, copyhistory=yes, width=600, height=450,top=100,left=350'
        window.open(url, '_blank', option)
      }
      const href = encodeURIComponent(document.location.href) || `${this.href}`
      const title = this.title
      switch (type) {
        case 'facebook': // 分享到Facebook的代码
          toOpen('http://www.facebook.com/sharer.php?u=' + href + '&t=' + title)
          break
        case 'twitter': // 分享到twitter的代码
          toOpen('http://twitter.com/home?status=' + href + ' ' + title)
          break
        case 'ins': // 分享到ins
          toOpen('http://www.linkedin.com/shareArticle?mini=true&url=' + href + '&title=' + title)
          break
      }
    },
    share(){
      if(
        window.webkit && window.webkit.messageHandlers && window.webkit.messageHandlers.share && window.webkit.messageHandlers.share.postMessage
      ){
        window.webkit.messageHandlers.share.postMessage({"url" : "https://www.google.com"});
      }else{
        this.showCard = true;
      }
    }
  },
}
</script>

<style lang="css" scoped>
 .wrap{
  display: flex;
  flex-flow: row nowrap;
  justify-content: center;
 }
</style>
