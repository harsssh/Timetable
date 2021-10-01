<template>
  <el-row type="flex" class="row-bg" :gutter="10">
    <el-col :span="4">
      <div class="col-container white" :class="weekStyle()">{{ week }}</div>
    </el-col>

    <el-col :span="5">
      <div class="col-container bg-purple-light">a</div>
    </el-col>
    <el-col :span="5">
      <div class="col-container bg-purple">a</div>
    </el-col>
    <el-col :span="5">
      <div class="col-container bg-purple-light">a</div>
    </el-col>
    <el-col :span="5">
      <div class="col-container bg-purple">a</div>
    </el-col>
  </el-row>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class Week extends Vue {
  @Prop() private week!: string

  weekStyle(): string | undefined {
    if (this.week === '月') {
      return 'week-mon'
    }
    if (this.week === '火') {
      return 'week-tue'
    }
    if (this.week === '水') {
      return 'week-wed'
    }
    if (this.week === '木') {
      return 'week-thu'
    }
    if (this.week === '金') {
      return 'week-fri'
    }
  }
}
</script>

<style>
.el-col {
  border-radius: 4px;
}

.el-row {
  margin-bottom: 10px;
}

.el-row:last-child {
  margin-bottom: 0;
}
</style>

<style scoped>
.bg-purple {
  background: #d3dce6;
}

.bg-purple-light {
  background: #e5e9f2;
}

.col-container {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  min-height: 36px;
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
  font-size: 20px;
}
.week-mon {
  background-color: #db4125;
}

.week-tue {
  background-color: #33a1dc;
}

.week-wed {
  background-color: #0ba299;
}

.week-thu {
  background-color: #e3831c;
}

.week-fri {
  background-color: #83b427;
}
</style>
