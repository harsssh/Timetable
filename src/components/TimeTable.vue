<template>
  <div class="time-table-container">
    <DayHeader />
    <Day v-for="day in days" :key="day" :day="day" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Day from './Day.vue'
import DayHeader from './DayHeader.vue'

@Component({
  components: {
    Day,
    DayHeader,
  },
})
export default class TimeTable extends Vue {
  days = [0, 1, 2, 3, 4]
}
</script>

<style scoped>
h1 {
  margin: 0;
}

.day-container {
  margin-bottom: 5px;
}
.day-container:last-child {
  margin-bottom: 0;
}

.day-header-container {
  margin-bottom: 10px;
}
</style>
