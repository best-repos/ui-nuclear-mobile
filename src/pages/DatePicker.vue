<template>
  <div class="date-picker-list">
    <div class="demoTitle">Basic</div>
    <List>
      <DatePicker
        :onDismiss="dismiss"
        mode="datetime"
        v-model="date">
        <template slot-scope="props" slot="list-item">
          <ListItem arrow="horizontal" :extra="props.extra">Datetime</ListItem>
        </template>
      </DatePicker>

      <DatePicker
        :onDismiss="dismiss"
        v-model="dateA">
        <template slot-scope="props" slot="list-item">
          <ListItem arrow="horizontal" :extra="props.extra">Date</ListItem>
        </template>
      </DatePicker>

      <DatePicker
        :onDismiss="dismiss"
        :use12Hours="true"
        mode="time"
        v-model="dateB">
        <template slot-scope="props" slot="list-item">
          <ListItem arrow="horizontal" :extra="props.extra">Time (am/pm)</ListItem>
        </template>
      </DatePicker>

      <DatePicker
        :onDismiss="dismiss"
        mode="time"
        :minDate="minDate"
        :maxDate="maxDate"
        v-model="dateC">
        <template slot-scope="props" slot="list-item">
          <ListItem arrow="horizontal" :extra="props.extra">Limited time</ListItem>
        </template>
      </DatePicker>

      <DatePicker
        :onDismiss="dismiss"
        mode="time"
        format="'UTC Time: 'HH:MM"
        v-model="dateD">
        <template slot-scope="props" slot="list-item">
          <ListItem arrow="horizontal" :extra="props.extra">UTC time</ListItem>
        </template>
      </DatePicker>

      <DatePicker
        :onDismiss="dismiss"
        :locale="localCN"
        extra=" "
        mode="datetime"
        v-model="dateE"
        ref="datePickerControlVisible">
        <template slot-scope="props" slot="list-item">
          <ListItem :onClick="clickControlVisible" :extra="props.extra">External control visible state</ListItem>
        </template>
      </DatePicker>

      <DatePicker
        :onDismiss="dismiss"
        :locale="localCN"
        :onValueChange="valueChange"
        @change="change"
        mode="time"
        extra="click to choose"
        title="Select Time"
        v-model="dateChild">
        <template slot-scope="props">
          <div style="background-color: rgb(255, 255, 255); height: 45px; line-height: 45px; padding: 0px 15px;">
            With customized children
            <span style="float: right; color: rgb(136, 136, 136);">{{dateChild ? dateformat(dateChild, 'HH:MM') : 'click to choose'}}</span>
          </div>
        </template>
      </DatePicker>
    </List>

    <div class="demoTitle">With form validation</div>
    <List>
      <InputItem
        v-model="inputDate"
        placeholder="must be the format of YYYY-MM-DD"
        :error="hasError"
        :initialValue="initialValue"
        @input="computedDate">Input date</InputItem>
      <DatePicker
        :onDismiss="dismiss"
        :locale="localCN"
        :onOk="inputOk"
        mode="datetime"
        extra=""
        v-model="dateF">
        <template slot-scope="props" slot="list-item">
          <ListItem arrow="horizontal" :extra="props.extra">Date</ListItem>
        </template>
      </DatePicker>
      <ListItem>
        <Button type="primary" size="small" :onClick="submitInput" :inline="true">Submit</Button>
        <Button size="small" :inline="true" :onClick="resetInput">Reset</Button>
      </ListItem>
    </List>
  </div>
</template>
<script>
import {List, ListItem} from '@/components/List'
import DatePicker from '@/components/DatePicker'
import dateformat from 'dateformat'
import InputItem from '@/components/InputItem'
import Button from '@/components/Button'
export default {
  name: 'DatePickerPage',
  components: {
    List,
    ListItem,
    DatePicker,
    InputItem,
    Button
  },
  data () {
    return {
      localCN: {
        datePickerLocale: {
          year: '年',
          month: '月',
          day: '日',
          hour: '时',
          minute: '分',
          am: '上午',
          pm: '下午'
        },
        okText: '确定',
        dismissText: '取消'
      },
      date: new Date(),
      dateA: new Date(),
      dateB: new Date(),
      dateC: new Date(),
      dateD: new Date(),
      dateE: null,
      dateChild: null,
      dateF: new Date(),
      inputDate: dateformat(new Date(), 'yyyy-mm-dd'),
      initialValue: dateformat(new Date(), 'yyyy-mm-dd'),
      minDate: new Date(dateformat(new Date(), 'yyyy-mm-dd') + ' ' + '09:30'),
      maxDate: new Date(dateformat(new Date(), 'yyyy-mm-dd') + ' ' + '16:15'),
      hasError: false
    }
  },
  methods: {
    dateformat (date, format) {
      return dateformat(date, format)
    },
    dismiss () {},
    clickControlVisible () {
      this.$refs.datePickerControlVisible.maskClosable = false
    },
    valueChange (val, index) {
      console.log(val, index)
    },
    change (date) {
      console.log('changed', date)
    },
    submitInput () {
      console.log({idp: this.inputDate, dp: new Date(this.dateF)})
      if (this.hasError) {
        alert('Validation failed')
      }
    },
    resetInput () {
      this.inputDate = dateformat(new Date(), 'yyyy-mm-dd')
      this.dateF = new Date()
    },
    computedDate () {
      let date = new Date()
      this.hasError = false
      try {
        let dateString = `${dateformat(new Date(this.inputDate), 'yyyy-mm-dd')} ${dateformat(new Date(), 'HH:MM')}`
        date = new Date(dateString)
      } catch (e) {
        this.hasError = true
      }
      this.dateF = date
    },
    inputOk (date) {
      this.inputDate = dateformat(date, 'yyyy-mm-dd')
    }
  },
  created () {
  }
}
</script>
<style scoped>
.demoTitle {
  padding: 15px 0 9px 15px;
  color: #000;
  font-size: 16px;
  line-height: 16px;
  height: 16px;
  font-weight: bolder;
  position: relative;
}
</style>
