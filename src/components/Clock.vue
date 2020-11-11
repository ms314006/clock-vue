<template>
  <div class="clock">
    <div class="hour" :style="{ transform: `rotateZ(${ hourAngle }deg)` }" />
    <div class="min" :style="{ transform: `rotateZ(${ minAngle }deg)` }" />
    <div class="sec" :style="{ transform: `rotateZ(${ secAngle }deg)` }" />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import Clock from '@/class/Clock';

export default {
  setup() {
    const hourAngle = ref(0);
    const minAngle = ref(0);
    const secAngle = ref(0);

    const updateNeedleAngle = () => {
      const clock = new Clock();
      secAngle.value = clock.getSecondAngle();
      minAngle.value = clock.getMinuteAngle();
      hourAngle.value = clock.getHourAngle();
    };

    onMounted(() => {
      updateNeedleAngle();
      setInterval(updateNeedleAngle, 1000);
    });

    return { hourAngle, minAngle, secAngle };
  },
};
</script>

<style lang="scss" scoped>
.clock {
  width: 350px;
  height: 350px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: url('../assets/img/clock.png');
  background-size: cover;
  border: 4px solid #091921;
  border-radius: 50%;
  box-shadow: 0 -15px 15px rgba(255, 255, 255, 0.05),
              inset 0 -15px 15px rgba(255, 255, 255, 0.05),
              0 15px 15px rgba(0, 0, 0, 0.3),
              inset 0 15px 15px rgba(0, 0, 0, 0.3);

  &::before {
    content: '';
    width: 15px;
    height: 15px;
    background: #fff;
    border-radius: 50%;
    z-index: 10000;
  }

  .hour, .min, .sec {
    position: absolute;
    display: flex;
    justify-content: center;
  }

  .hour {
    width: 160px;
    height: 160px;
  }

  .hour:before {
    content: '';
    position: absolute;
    width: 8px;
    height: 80px;
    background: #ff105e;
    z-index: 10;
    border-radius: 6px 6px 0 0;
  }

  .min {
    width: 190px;
    height: 190px;
  }

  .min:before {
    content: '';
    position: absolute;
    width: 4px;
    height: 90px;
    background: #fff;
    z-index: 11;
    border-radius: 6px 6px 0 0;
  }

  .sec {
    width: 230px;
    height: 230px;
  }

  .sec:before {
    content: '';
    position: absolute;
    width: 2px;
    height: 150px;
    background: #fff;
    z-index: 12;
    border-radius: 6px 6px 0 0;
  }
}
</style>
