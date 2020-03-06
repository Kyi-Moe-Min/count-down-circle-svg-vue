<template>
  <svg width="100" height="100" viewBox=" -5 -5 110 110">
    <!--   to get arc eqution. length/pi -->
    <defs>
      <linearGradient id="linear1">
        <stop offset="0" stop-color="yellow"></stop>
        <stop offset="100" stop-color="green"></stop>
      </linearGradient>
      <linearGradient id="linear2">
        <stop offset="0" stop-color="yellow"></stop>
        <stop offset="100" stop-color="red"></stop>
      </linearGradient>
      <mask id="mask">
        <path :d="countDownArcPath" stroke="white" stroke-width="40" fill="transparent"></path>
      </mask>
    </defs>
    <path
      mask="url(#mask)"
      :d="arc1Path"
      stroke="url(#linear1)"
      stroke-width="10"
      fill="transparent"
    ></path>
    <path
      mask="url(#mask)"
      :d="arc2Path"
      stroke="url(#linear2)"
      stroke-width="10"
      fill="transparent"
    ></path>
  </svg>
</template>
<script>
const size = 100;
const RADIUS = size / 2;
let intervalId = 0;
export default {
  name: "CountDownCircle",
  data() {
    return {
      degree: 0,
      interval: 1000
    };
  },
  computed: {
    arc1Path() {
      return `M ${RADIUS *
        2} ${RADIUS} A ${RADIUS} ${RADIUS} 90 0 0 0 ${RADIUS}`;
    },
    arc2Path() {
      return `M 0 ${RADIUS} A ${RADIUS} ${RADIUS} 90 0 0 ${RADIUS *
        2} ${RADIUS}`;
    },
    largeFlag() {
      return this.degree > 180 ? 0 : 1;
    },
    countDownArcPath() {
      const { x, y } = this.countDownArc;
      const largeFlag = this.largeFlag;
      return `M ${x} ${y} A ${RADIUS} ${RADIUS} 90 ${largeFlag} 0 ${RADIUS *
        2} ${RADIUS + 0}`;
    },
    radian() {
      return (Math.PI * -this.degree) / 180;
    },
    x() {
      return Math.cos(this.radian) * RADIUS;
    },
    y() {
      return Math.sin(this.radian) * RADIUS;
    },
    countDownArc() {
      return {
        x: this.x + RADIUS,
        y: this.y + RADIUS
      };
    }
  },
  methods: {
    rotate() {
      intervalId = setInterval(() => {
        console.log(this.countDownArcPath);
        if (this.degree >= 360) {
          clearInterval(intervalId);
          intervalId = 0;
        } else this.degree += 10;
      }, this.interval);
    }
  },
  mounted() {
    this.rotate();
  }
};
</script>
<style scoped>
path {
  transition: d 0.5s;
}
svg {
  transform: rotate(-90deg);
}
</style>
