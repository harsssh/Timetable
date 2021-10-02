<template>
  <div class="day-container">
    <el-row type="flex" class="row-bg" :gutter="10">
      <el-col :span="4">
        <div class="content-container white day" :class="weekStyle()">
          {{ weekDays[day] }}
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple-light">
          <CourseCard />
        </div>
      </el-col>
      <el-col :span="5">
        <div class="content-container bg-purple">
          <i class="add el-icon-plus"></i>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="content-container bg-purple-light">
          <i class="add el-icon-plus"></i>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="content-container bg-purple">
          <i class="add el-icon-plus"></i>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import CourseCard from './CourseCard.vue'

@Component({
  components: {
    CourseCard,
  },
})
export default class Week extends Vue {
  @Prop() private day!: number

  weekDays = ['月', '火', '水', '木', '金']
  weekDaysEn = ['mon', 'tue', 'wed', 'thu', 'fri']

  weekStyle(): string {
    return 'day-' + this.weekDaysEn[this.day]
  }
}
</script>

<style lang="scss" scoped>
$purple: #d3dce6;
$purple-light: #e5e9f2;
$hover-blue: #49a4ff;

.add {
  font-size: 17px;
  padding: 7px;
  border-radius: 50%;
  cursor: pointer;

  &:hover {
    color: $hover-blue;
    border-color: desaturate($hover-blue, 40%) !important;
    background: rgba($hover-blue, 0.07);
  }
}

.bg-purple .add {
  border: 1px solid darken($purple, 30%);
}

.bg-purple-light .add {
  border: 1px solid darken($purple-light, 30%);
}

.course-card-container {
  width: 100%;
}

.el-col {
  display: flex;
  justify-content: center;
  align-items: center;

  min-height: 195px;
}

.content-container {
  display: flex;
  justify-content: center;
  align-items: center;

  border-radius: 4px;
  height: 100%;
  width: 100%;
}

.day {
  height: 65%;
  width: 65%;
}

.el-col {
  border-radius: 4px;
}

.bg-purple {
  background: $purple;
}

.bg-purple-light {
  background: $purple-light;
}

.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}

.bg-purple-dark {
  background: #99a9bf;
}

.white {
  font-weight: bold;
  color: #f3f3f3;
  font-size: 24px;
}
.day-mon {
  background-color: #db4125;
}

.day-tue {
  background-color: #33a1dc;
}

.day-wed {
  background-color: #0ba299;
}

.day-thu {
  background-color: #e3831c;
}

.day-fri {
  background-color: #83b427;
}
</style>
