<template>
  <div class="week-header-container">
    <el-row type="flex" class="row-bg" :gutter="10">
      <el-col :span="4">
        <div class="col-container black bg-purple-dark">曜日</div>
      </el-col>

      <el-col :span="5">
        <div class="col-container bg-purple-light">
          <el-popover
            placement="top"
            title="授業時間"
            width="200"
            trigger="hover"
            content="8:50-10:30"
          >
            <span slot="reference">1・2限</span>
          </el-popover>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="col-container bg-purple">
          <el-popover
            placement="top"
            title="授業時間"
            width="200"
            trigger="hover"
            content="10:40-12:20"
          >
            <span slot="reference">3・4限</span>
          </el-popover>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="col-container bg-purple-light">
          <el-popover
            placement="top"
            title="授業時間"
            width="200"
            trigger="hover"
            content="14:20-16:00"
          >
            <span slot="reference">5・6限</span>
          </el-popover>
        </div>
      </el-col>
      <el-col :span="5">
        <div class="col-container bg-purple">
          <el-popover
            placement="top"
            title="授業時間"
            width="200"
            trigger="hover"
            content="16:15-17:55"
          >
            <span slot="reference">7・8限</span>
          </el-popover>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class WeekHeader extends Vue {}
</script>

<style></style>

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

.black {
  font-weight: bold;
  color: #414141;
  font-size: 20px;
}
</style>
