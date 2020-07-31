<template>
  <div id="grad">
    <section
      class="title text-3xl flex justify-center content-center flex-col mx-auto text-center"
    >Fast Zuhause</section>
    <section class="calc date flex text-6xl justify-center content-center">
      <div class="overlay"></div>
      <div class="days mr-2 relative">
        {{disDays}}
        <div class="label text-sm text-center bottom-0">Tage</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="hours mx-2 relative">
        {{disHours}}
        <div class="label text-sm text-center bottom-0">Stunden</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="minutes mx-2 relative">
        {{disMinutes}}
        <div class="label text-sm text-center bottom-0">Minuten</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="seconds ml-2 relative">
        {{disSeconds}}
        <div class="label text-sm text-center bottom-0">Sekunden</div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data: () => ({
    disDays: 0,
    disHours: 0,
    disMinutes: 0,
    disSeconds: 0,
  }),
  computed: {
    _sec: () => 1000,
    _min() {
      return this._sec * 60
    },
    _hr() {
      return this._min * 60
    },
    _day() {
      return this._hr * 24
    },
  },
  mounted() {
    this.showRem()
  },
  methods: {
    formatNum(num) {
      return num < 10 ? '0' + num : num
    },
    showRem() {
      const timer = setInterval(() => {
        const now = new Date()
        const end = new Date(2020, 8, 2, 8, 15, 0, 0)
        const distance = end.getTime() - now.getTime()

        if (distance < 0) {
          clearInterval(timer)
          return
        }
        const days = Math.floor(distance / this._day)
        const hours = Math.floor((distance % this._day) / this._hr)
        const minutes = Math.floor((distance % this._hr) / this._min)
        const seconds = Math.floor((distance % this._min) / this._sec)
        this.disMinutes = this.formatNum(minutes)
        this.disSeconds = this.formatNum(seconds)
        this.disHours = this.formatNum(hours)
        this.disDays = this.formatNum(days)
      }, 1000)
    },
  },
}
</script>

<style>
* {
  font-family: 'Major Mono Display', monospace;
  color: #fff;
}
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  background-color: rgba(0, 0, 0, 0.4);
}
#grad {
  background-image: linear-gradient(
    rgba(24, 24, 24, 1),
    rgba(200, 26, 26, 0.9),
    rgba(233, 236, 39, 1)
  );
  padding: 20px;
}
.title {
  position: fixed;
  z-index: 10;
}
.label {
  font-weight: bold;
  margin-top: 0;
}
.calc {
  padding-top: 40px;
}
.seconds {
  max-width: 50px;
}
</style>