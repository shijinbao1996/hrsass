<template>
  <div>
    <el-row type="flex" justify="end">
      <el-select
        v-model="currentYear"
        size="small"
        style="width: 120px"
        @change="uploadChange"
      >
        <el-option
          v-for="item in yearList"
          :key="item"
          :label="item"
          :value="item"
          >{{ item }}</el-option
        >
      </el-select>
      <el-select
        v-model="currentMonth"
        size="small"
        style="width: 120px; margin-left: 10px"
        @change="uploadChange"
      >
        <el-option v-for="item in 12" :key="item" :label="item" :value="item">{{
          item
        }}</el-option>
      </el-select>
    </el-row>
    <el-calendar v-model="currentDate">
      <template v-slot:dateCell="{ date }">
        <div class="cell-box">
          {{ date.getDate() }}
          <span v-if="isWeek(date)">休</span>
        </div>
      </template>
    </el-calendar>
  </div>
</template>

<script>
export default {
  name: 'Calendar',
  props: {
    startDate: {
      type: Date,
      default: () => new Date()
    }
  },
  data() {
    return {
      currentMonth: null, // 当前月份
      currentYear: null, // 当前年份
      currentDate: null,
      yearList: []
    }
  },
  methods: {
    initCalendar() {
      const date = new Date()
      this.currentYear = date.getFullYear()
      this.currentMonth = date.getMonth() + 1
      this.yearList = Array(11)
        .fill(this.currentYear - 5)
        .map((item, i) => {
          return item + i
        })
      console.log(this.yearList)
    },
    isWeek(date) {
      return date.getDay() === 6 || date.getDay() === 0
    },
    uploadChange() {
      this.currentDate = this.currentYear + '-' + this.currentMonth
    }
  },
  created() {
    this.initCalendar()
  }
}
</script>

<style scoped lang="scss">
::v-deep .el-calendar__header {
  display: none;
}
::v-deep .el-calendar-table__row .current,
::v-deep .el-calendar-table__row .next {
  border: none !important;
}
.cell-box {
  display: flex;
  align-items: center;
  justify-content: center;
  color: orange;
  height: 100%;
}
</style>
