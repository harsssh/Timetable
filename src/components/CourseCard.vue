<template>
  <div class="course-card-container">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>{{ name }}</span>
        <el-button style="float: right; padding: 3px 0" type="text"
          >編集</el-button
        >
      </div>

      <div class="items">
        <div class="text item">
          <p class="item-header">講義室</p>
          <p>{{ room }}</p>
        </div>
        <div class="text item">
          <p class="item-header">担当教員</p>
          <p>{{ instructor }}</p>
        </div>
      </div>

      <el-divider direction="vertical"></el-divider>

      <div class="button-container">
        <el-button
          type="primary"
          round
          :href="url"
          target="_blank"
          :disabled="isUrlEmpty"
          >参加</el-button
        >
      </div>
    </el-card>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class WeekHeader extends Vue {
  @Prop({ required: true }) name: string
  @Prop({ required: true }) room: string
  @Prop({ required: true }) instructor: string
  @Prop({ required: true }) url: string

  get isUrlEmpty(): boolean {
    return this.url === ''
  }
}
</script>

<style>
.el-card__body {
  display: flex;
}
</style>

<style scoped>
.course-card-container {
  width: 100%;
  height: 100%;
}

.el-divider {
  height: auto;
}

.items {
  padding-left: 20px;
  padding-right: 15px;
}

.items p {
  margin: 0;
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;

  width: 100%;
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
