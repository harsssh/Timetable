<template>
  <div class="course-card-container">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <span>{{ name }}</span>
        <el-button
          style="float: right; padding: 3px 0"
          type="text"
          @click="dialogVisible = true"
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
          @click="joinZoom"
          >参加</el-button
        >
      </div>
    </el-card>

    <el-dialog title="講義情報" :visible.sync="dialogVisible">
      <el-form :model="editForm">
        <el-form-item label="科目名">
          <el-input v-model="editForm.name" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="講義室">
          <el-input v-model="editForm.room" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="指導教員">
          <el-input v-model="editForm.instructor" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="Zoom URL">
          <el-input v-model="editForm.url" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>

      <span slot="footer" class="dialog-footer">
        <el-button type="danger" @click="deleteData">削除</el-button>
        <el-button type="primary" @click="editSubmit">更新</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component
export default class CourseCard extends Vue {
  @Prop({ required: true }) name!: string
  @Prop({ required: true }) room!: string
  @Prop({ required: true }) instructor!: string
  @Prop({ required: true }) url!: string

  dialogVisible = false

  editForm = {
    name: this.name,
    room: this.room,
    instructor: this.instructor,
    url: this.url,
  }

  get isUrlEmpty(): boolean {
    return this.url === ''
  }

  editSubmit(): void {
    this.$emit('update:name', this.editForm.name)
    this.$emit('update:room', this.editForm.room)
    this.$emit('update:instructor', this.editForm.instructor)
    this.$emit('update:url', this.editForm.url)

    this.dialogVisible = false

    this.$message({
      message: '講義情報を更新しました。',
      type: 'success',
    })
  }

  joinZoom(): void {
    window.open(this.url, '_blank')
  }

  deleteData(): void {
    this.$emit('delete')
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
