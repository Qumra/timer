<template>

  <span style="color: #ff0000; font-weight: 700"><span v-if="hour!=='00'">{{ hour}}小时</span>{{ min }}分钟{{ sec }}秒</span>

</template>

<script>

export default {
  name: 'ExamTimer',
  props: {
    value: Number
  },

  data() {
    return {
      leftSeconds:0,
      hour:'00',
      min: '00',
      sec: '00',
      timer:null
    }
  },

  // watch: {
  //   value: {
  //     handler() {
  //       this.leftSeconds = this.value
  //       this.countdown()
  //     }
  //   }
  // },

  created() {
    // this.leftSeconds = this.value
    // let limitTime = localStorage.getItem('limitTime')
    // this.leftSeconds = (new Date(limitTime).getTime() - new Date().getTime())/1000
    this.leftSeconds = localStorage.getItem('leftSeconds')
    console.log(this.leftSeconds)
  },
  mounted() {
			this.countdown()
		},
  beforeDestroy(){
    // clearTimeout(this.timer)
  },
  methods: {

    // 进行倒计时
    countdown() {
      console.log('倒计时开始。。。',this.leftSeconds)
    //   // 倒计时结束了
    //   if (this.leftSeconds <= 0) {
    //     this.$emit('timeout')
    //     return
    //   }

    //   // 时
    //   const min = parseInt(this.leftSeconds / 60)
    //   const sec = parseInt(this.leftSeconds % 60)

    //   this.min = min > 9 ? min : '0' + min
    //   this.sec = sec > 9 ? sec : '0' + sec
    //   this.leftSeconds -= 1
    //   localStorage.setItem('leftSeconds',this.leftSeconds)
    //   const that = this
    // this.timer =  setTimeout(function() {
    //     that.countdown()
    //   }, 1000)
    let self = this;
    let timer = setInterval(function(){
       if (self.leftSeconds > 0) {
          // 时
        const hour = parseInt(self.leftSeconds / 60 / 60 % 24)
        const min = parseInt(self.leftSeconds / 60 % 60)
        const sec = parseInt(self.leftSeconds % 60)
        self.hour = hour > 9 ? hour : '0' + hour
        self.min = min > 9 ? min : '0' + min
        self.sec = sec > 9 ? sec : '0' + sec
        self.leftSeconds -= 1
        // localStorage.setItem('leftSeconds',self.leftSeconds)
       }else{
         self.$emit('timeout')
        clearInterval(timer);
       }
    },1000)
    }

  }
}
</script>

