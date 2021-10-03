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
          <CourseCard
            v-if="existData('period1')"
            :name="courses.period1.name"
            :room="courses.period1.room"
            :instructor="courses.period1.instructor"
            :url="courses.period1.url"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period1')"></i>
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple">
          <CourseCard
            v-if="existData('period3')"
            :name="courses.period3.name"
            :room="courses.period3.room"
            :instructor="courses.period3.instructor"
            :url="courses.period3.url"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period3')"></i>
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple-light">
          <CourseCard
            v-if="existData('period5')"
            :name="courses.period5.name"
            :room="courses.period5.room"
            :instructor="courses.period5.instructor"
            :url="courses.period5.url"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period5')"></i>
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple">
          <CourseCard
            v-if="existData('period7')"
            :name="courses.period7.name"
            :room="courses.period7.room"
            :instructor="courses.period7.instructor"
            :url="courses.period7.url"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period7')"></i>
        </div>
      </el-col>
    </el-row>

    <el-dialog title="講義情報" :visible.sync="dialogVisible">
      <el-form :model="form">
        <el-form-item label="科目名">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="講義室">
          <el-input v-model="form.room" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="指導教員">
          <el-input v-model="form.instructor" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="Zoom URL">
          <el-input v-model="form.url" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>

      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">キャンセル</el-button>
        <el-button type="primary" @click="submit">登録</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import CourseCard from './CourseCard.vue'

interface CourseData {
  [key: string]: {
    name: string
    room: string
    instructor: string
    url: string
  }
}

@Component({
  components: {
    CourseCard,
  },
})
export default class Day extends Vue {
  @Prop() private day!: number

  weekDays = ['月', '火', '水', '木', '金']
  weekDaysEn = ['mon', 'tue', 'wed', 'thu', 'fri']

  dialogVisible = false

  form = {
    name: '',
    room: '',
    instructor: '',
    url: '',
  }

  editing = ''
  courses: CourseData = {}

  weekStyle(): string {
    return 'day-' + this.weekDaysEn[this.day]
  }

  showDialog(period: string): void {
    this.editing = period
    this.dialogVisible = true
  }

  submit(): void {
    Object.keys(this.form).forEach((key) => {
      if (key === 'url') return

      if (this.form[key] === '') this.form[key] = '未設定'
    })

    this.courses[this.editing] = this.form

    this.editing = ''
    this.dialogVisible = false
  }

  existData(period: string): boolean {
    return period in this.courses
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
