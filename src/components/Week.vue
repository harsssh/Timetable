<template>
  <el-row type="flex" class="row-bg" :gutter="10">
    <el-col :span="4">
      <div class="content bg-purple-dark">{{ week }}</div>
    </el-col>

    <el-col :span="5">
      <div class="content bg-purple">a</div>
    </el-col>
    <el-col :span="5">
      <div class="content bg-purple-light">a</div>
    </el-col>
    <el-col :span="5">
      <div class="content bg-purple">a</div>
    </el-col>
    <el-col :span="5">
      <div class="content bg-purple-light">a</div>
    </el-col>
  </el-row>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class TimeTable extends Vue {
  @Prop() private week!: string
}
</script>

<style>
.el-col {
  border-radius: 4px;
}
</style>

<style scoped>
.bg-purple-dark {
  background: #99a9bf;
}
.bg-purple {
  background: #d3dce6;
}
.bg-purple-light {
  background: #e5e9f2;
}

.content {
  border-radius: 4px;
  min-height: 36px;
}

.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
</style>
