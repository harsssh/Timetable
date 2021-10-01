<template>
  <div class="time-table-conteiner">
    <h1>2021 3Q</h1>
    <Week :week="weekDays[0]"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Week from './Week'

@Component({
  components: {
    Week,
  },
})
export default class TimeTable extends Vue {
  weekDays = ['月', '火', '水', '木', '金']
}
</script>

<style scoped></style>
