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
            :name.sync="courses.period1.name"
            :room.sync="courses.period1.room"
            :instructor.sync="courses.period1.instructor"
            :url.sync="courses.period1.url"
            @delete="deleteData('period1')"
            @update="updateData"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period1')"></i>
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple">
          <CourseCard
            v-if="existData('period2')"
            :name.sync="courses.period2.name"
            :room.sync="courses.period2.room"
            :instructor.sync="courses.period2.instructor"
            :url.sync="courses.period2.url"
            @delete="deleteData('period2')"
            @update="updateData"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period2')"></i>
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple-light">
          <CourseCard
            v-if="existData('period3')"
            :name.sync="courses.period3.name"
            :room.sync="courses.period3.room"
            :instructor.sync="courses.period3.instructor"
            :url.sync="courses.period3.url"
            @delete="deleteData('period3')"
            @update="updateData"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period3')"></i>
        </div>
      </el-col>

      <el-col :span="5">
        <div class="content-container bg-purple">
          <CourseCard
            v-if="existData('period4')"
            :name.sync="courses.period4.name"
            :room.sync="courses.period4.room"
            :instructor.sync="courses.period4.instructor"
            :url.sync="courses.period4.url"
            @delete="deleteData('period4')"
            @update="updateData"
          />
          <i v-else class="add el-icon-plus" @click="showDialog('period4')"></i>
        </div>
      </el-col>
    </el-row>

    <el-dialog title="講義情報" :visible.sync="dialogVisible">
      <el-form :model="form">
        <el-form-item label="講義名">
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
        <el-button type="primary" @click="submit">追加</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'
import CourseCard from './CourseCard.vue'

interface Keys {
  name: string
  room: string
  instructor: string
  url: string
}

interface CourseData {
  [key: string]: Keys
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

  dayEn = this.weekDaysEn[this.day]

  dialogVisible = false

  form = {
    name: '',
    room: '',
    instructor: '',
    url: '',
  } as Keys

  editing = ''
  courses: CourseData = {}

  created(): void {
    const store = localStorage.getItem(this.dayEn)
    if (store) {
      this.courses = JSON.parse(store)
    }
  }

  weekStyle(): string {
    return 'day-' + this.dayEn
  }

  showDialog(period: string): void {
    this.editing = period
    this.dialogVisible = true
  }

  submit(): void {
    if (this.form.name === '') this.form.name = '未設定'
    if (this.form.room === '') this.form.room = '未設定'
    if (this.form.instructor === '') this.form.instructor = '未設定'

    this.courses[this.editing] = { ...this.form }

    // localStorage
    localStorage.setItem(this.dayEn, JSON.stringify(this.courses))

    // 初期化
    this.dialogVisible = false
    this.editing = ''

    this.form.name = ''
    this.form.room = ''
    this.form.instructor = ''
    this.form.url = ''

    this.$message({
      message: '講義が追加されました。',
      type: 'success',
    })
  }

  existData(period: string): boolean {
    return period in this.courses
  }

  deleteData(period: string): void {
    this.$delete(this.courses, period)

    // localStorage
    localStorage.setItem(this.dayEn, JSON.stringify(this.courses))

    this.$message({
      message: '講義が削除されました。',
      type: 'success',
    })
  }

  updateData(): void {
    localStorage.setItem(this.dayEn, JSON.stringify(this.courses))

    this.$message({
      message: '講義情報を更新しました。',
      type: 'success',
    })
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

  min-height: 150px;
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
