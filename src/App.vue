<template>
  <div id="clock">
    <h2>The time is now</h2>
    <div id="time">
      <div>
        <span id="hour">{{ hour }}</span>
        <span>Hours</span>
      </div>
      <div>
        <span id="minute">{{ minute }}</span>
        <span>Minutes</span>
      </div>
      <div>
        <span id="second">{{ second }}</span>
        <span>Seconds</span>
      </div>
      <div>
        <span id="ampm">{{ ampm }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, toRefs, onMounted } from 'vue';
export default {
  setup() {
    const date = reactive({
      hour: '00',
      minute: '00',
      second: '00',
      ampm: 'AM',
    });

    onMounted(() => {
      let interval = setInterval(() => {
        clock(date);
      }, 1000);
    });

    return {
      ...toRefs(date),
    };
  },
};
function clock(date) {
  let h = new Date().getHours();
  let m = new Date().getMinutes();
  let s = new Date().getSeconds();
  let am = 'AM';
  if (h > 12) {
    am = 'PM';
  }
  h = h < 10 ? '0' + h : h;
  m = m < 10 ? '0' + m : m;
  s = s < 10 ? '0' + s : s;
  date.hour = h;
  date.minute = m;
  date.second = s;
  date.ampm = am;
}
</script>
