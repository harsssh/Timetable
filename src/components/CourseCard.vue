<template>
  <div class="course-card-container">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>授業名</span>
        <el-button style="float: right; padding: 3px 0" type="text"
          >編集</el-button
        >
      </div>

      <div class="items">
        <div class="text item">
          <p class="item-header">教室</p>
          <p>H000</p>
        </div>
        <div class="text item">
          <p class="item-header">担当教員</p>
          <p>野村 千咲</p>
        </div>
      </div>

      <div class="button-container">
        <el-button type="primary" round>Zoom</el-button>
        <el-button icon="el-icon-edit" circle></el-button>
      </div>
    </el-card>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class WeekHeader extends Vue {}
</script>

<style>
.el-card__body {
  display: flex;
}
</style>

<style scoped>
.el-button + .el-button {
  margin-left: 3px;
}

.items {
  padding: 0 15px;
}

.items p {
  margin: 0;
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.item-header {
  display: inline-block;
  width: 5em;
  font-weight: bold;
}

.text {
  font-size: 14px;
}

.item {
  margin-bottom: 10px;
}
.item:last-child {
  margin-bottom: 0;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: '';
}
.clearfix:after {
  clear: both;
}
</style>
