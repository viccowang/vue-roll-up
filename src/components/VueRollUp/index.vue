<template>
  <div class="vue-roll-up" :style="marqueeStyle">
    <ul
    :style="marqueeWrapperStyle"
    @mouseover="mouseoverHandle"
    @mouseleave="mouseleaveHandel"
    >
      <li
        v-for="(marquee,index) in marqueeList"
        :key="index"
        :style="marqueeLiStyle"
      >
        <template v-if="useSlot">
          <slot :marquee="marquee"></slot>
        </template>
        <template v-else>
          {{ marquee }}
        </template>
      </li>
    </ul>
  </div>
</template>
<script>
/**
 * Vue Roll Up
 * ===============
 * Author: Vicco Wang
 * Date: 2019.03.21
 *
 */
export default {
  name: 'VueRollUp',
  props: {
    // marquee list data
    rollList: {
      type: Array,
      default: function () {
        return []
      }
    },
    useSlot: {
      type: Boolean,
      default: false
    },
    // marquee width
    width: {
      default: 200
    },
    // marquee wrapper height = marquee height
    height: {
      type: Number,
      default: 35
    },
    // marquee color
    color: {
      type: String,
      default: '#333'
    },
    // marquee background color
    bgColor: {
      type: String,
      default: ''
    },
    // do not support in this version
    direction: {
      type: String,
      default: 'up'
    },
    // roll up duration
    duration: {
      type: Number,
      default: 2000
    },
    // roll up speed in millisecond
    speed: {
      type: Number,
      default: 1000
    }
  },
  computed: {
    marqueeListLength () {
      return this.marqueeList.length || 0
    },
    marqueeStyle () {
      return {
        width: this.isNumber(this.width) ? this.width + 'px' : this.width,
        height: this.height + 'px',
        backgroundColor: this.bgColor
      }
    },
    marqueeWrapperStyle () {
      return {
        transform: `translateY(${this.rollDistance}px)`,
        transitionDuration: `${this.transitionSpeed}ms`
      }
    },
    marqueeLiStyle () {
      return {
        ...this.marqueeStyle,
        color: this.color
      }
    }
  },
  watch: {
    rollList: {
      handler (data) {
        if (data && data.length) {
          // 为了保证无缝滚动的连续性，需要将最后一个和第一个滚动内部保持一致
          this.marqueeList = [
            ...data,
            data[0]
          ]
          this.resetRoll()
          // start to roll
          this.startToRoll()
        }
      },
      immediate: true
    }
  },
  data () {
    return {
      marqueeList: [],
      // 滚动距离,根据自定义行高度来动态计算
      rollDistance: 0,
      // 当前滚动到第几个，当滚动至最后一个后需要归零
      rollMarqueeIndex: 0,
      // 滚动速度
      transitionSpeed: 0,
      // 滚动延迟时的setInterval
      rollIntervalTimer: null,
      rollTimeoutTimer: null
    }
  },
  mounted () {
  },
  methods: {
    rolling (height, transitionSpeed) {
      this.transitionSpeed = transitionSpeed
      this.rollDistance = height
    },
    resetRoll () {
      this.rollMarqueeIndex = 0
      this.rollDistance = 0
      if (this.rollIntervalTimer) {
        clearInterval(this.rollIntervalTimer)
        clearTimeout(this.rollTimeoutTimer)
      }
    },
    startToRoll () {
      this.rollIntervalTimer = setInterval(() => {
        this.rolling(++this.rollMarqueeIndex * -this.height, this.speed)
        if (this.rollMarqueeIndex === this.marqueeListLength - 1) {
          this.rollTimeoutTimer = setTimeout(() => {
            this.rolling(0, 0)
            this.rollMarqueeIndex = 0
          }, this.speed)
        }
      }, this.duration)
    },
    mouseoverHandle () {
      this.rollIntervalTimer && clearInterval(this.rollIntervalTimer)
    },
    mouseleaveHandel () {
      this.startToRoll()
    },
    isNumber (number) {
      return typeof number === 'number' && !isNaN(number)
    }
  }
}
</script>
<style lang="scss" scoped>
.vue-roll-up {
  position: relative;
  overflow: hidden;
  ul {
    padding: 0;
    margin: 0;
    width:100%;
    position: absolute;
    display: flex;
    flex-direction: column;
    transition: all .3s ease 0s;
    transform: translateY();
    transition-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
    li {
      display: inherit;
      list-style: none;
      align-items: center;
      overflow: hidden;
      transition: all .3s ease 0s;
      box-sizing: border-box;
    }
  }
}
</style>
