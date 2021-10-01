<template>
  <div class="time-table-container">
    <WeekHeader />
    <Week v-for="(week, id) in weekDays" :key="id" :week="week" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Week from './Week.vue'
import WeekHeader from './WeekHeader.vue'

@Component({
  components: {
    Week,
    WeekHeader,
  },
})
export default class TimeTable extends Vue {
  weekDays = ['月', '火', '水', '木', '金']
}
</script>

<style scoped></style>
