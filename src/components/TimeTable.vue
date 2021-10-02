<template>
  <div class="time-table-container">
    <WeekHeader />
    <Week v-for="day in days" :key="day" :day="day" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Week from './Day.vue'
import WeekHeader from './DayHeader.vue'

@Component({
  components: {
    Week,
    WeekHeader,
  },
})
export default class TimeTable extends Vue {
  days = [0, 1, 2, 3, 4]
}
</script>

<style scoped>
.day-container {
  margin-bottom: 15px;
}

.day-container:last-child {
  margin-bottom: 0;
}

.day-header-container {
  margin-bottom: 5px;
}
</style>
