<template>
  <section class="time-picker">
    <div class="hours">
      <div class="time-btns">
        <button @click="upHour">+</button>
        <button @click="downHour">-</button>
      </div>
      <p><span v-if="hour < 10">0</span>{{ hour }}:</p>
    </div>
    <div class="min">
      <p><span v-if="min < 10">0</span>{{ min }}</p>
      <div class="time-btns">
        <button @click="upMin">+</button>
        <button @click="downMin">-</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      hour: 12,
      min: 0,
    };
  },
  created() {},
  methods: {
    upHour() {
      this.hour++;
      if (this.hour === 25) this.hour = 1;
      this.setTime();
    },
    downHour() {
      this.hour--;
      if (this.hour === 0) this.hour = 24;
      this.setTime();
    },
    upMin() {
      this.min = this.min + 5;
      if (this.min > 59) {
        this.min = 0;
        this.hour++;
      }
      this.setTime();
    },
    downMin() {
      this.min = this.min - 5;
      if (this.min < 0) {
        this.min = 55;
        this.hour--;
      }
      this.setTime();
    },
    setTime() {
      let strHour = this.hour + "";
      let strMin = this.min + "";
      const newMin = strMin.padStart(2, "0");
      const newHour = strHour.padStart(2, "0");

      let time = `T${newHour}:${newMin}:00`;
      this.$emit("setTime", time);
    },
  },
};
</script>

<style>
</style>