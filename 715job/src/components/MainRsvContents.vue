<template>
<div>
  <div class="main-rsv-contents">
    <div class="rsv-text">
      <h1>
        예약 시각 선택
      </h1>
    </div>
    <div class="timecontents">
      <ul class="timeLists">
        <li v-for="i in 23" :key="i">
          <v-btn
            :id="'timetable-btn-'+i"
            class="timetable"
            elevation="0"
            :ripple="false"
            :color="colors[i]"
            @click="pickTime(i)"
            >{{ i }}
          </v-btn>
        </li>
      </ul>
    </div>
    <div class="rsv-text">
      <h1>
        예약 정보 입력
      </h1>
    </div>
    <div class="contents-row content-row-1">
      <div class="content-box">
        <span class="input-title"><span class="text-orangered">*</span> 예약 날짜</span>
        <input
        type="text"
        id="selectedDate"
        class="input-text-readonly"
        :value="RsvDate"
        readonly
      />
      </div>
      <div class="content-box">
        <span class="input-title"><span class="text-orangered">*</span> 예약자</span>
        <input class="input-text-readonly"  type="text" value="권용근" readonly />
      </div>
    </div>
    <div class="contents-row content-row-2" >
      <div class="content-box">
        <span class="input-title"><span class="text-orangered">*</span> 이용시작시각</span>
        <input class="input-text-readonly" type="text" :value="start_time+' : 00'" readonly />
      </div>
      <div style="margin-top:auto;margin-bottom:auto;">
        ~
      </div>
      <div class="content-box">
        <span class="input-title"><span class="text-orangered">*</span> 이용종료시각</span>
        <input class="input-text-readonly" type="text" :value="display_end_time+' : 00'" readonly />
      </div>
    </div>
    <div class="contents-row content-row-3">
      <div class="content-box">
        <span class="input-title"><span class="text-orangered">*</span> 이용 인원</span>
        <select class="peopleNum">
          <option>2</option>
          <option>3</option>
          <option>4</option>
        </select>
      </div>
      <div class="content-box">
        <span class="input-title"><span class="text-orangered">*</span> 테이블 번호</span>
        <input class="input-text-readonly" type="text" :value="'Table '+RsvTable" readonly />
      </div>
    </div>
    <div class="contents-row-last content-row-4">
        <span class="input-title">&nbsp;&nbsp;예약 내용</span>
        <textarea cols="2"></textarea>
    </div>
    <div class="rsv-text">
      <h1>유의사항</h1>
    </div>
    <div class="notice-contents">
      <div style="margin-bottom:24px;">
        <p>1. 715호 협업룸에서 이용한 물품 및 설비는 이용 후 반드시 제자리에 둔다.</p>
        <p>2. 715호 협업룸을 함께 이용하는 모두를 위해 이용 이후 반드시 주변 청결을 유지한다.</p>
        <p>3. 715호 협업룸을 같은 시각에 다른 팀과 함께 이용할 경우, 서로에게 방해가 되지 않도록 배려하며 이용한다.</p>
        <p>4. 715호 협업룸 이용 예약자 및 이용자는 715호 협업룸의 설비와 기물을 고장 및 파손에 대해 유의하며 이용한다.</p>
      </div>
    </div>
    <div class="confirm-note">
      <input class="confirm-note-checkbox" type="checkbox" v-model="isChecked" />
      <div class="confirm-note-text">위의 사항에 동의합니다.</div>
    </div>
    <div class="rsv-button">
      <router-link to="/rsvcomplete" style="text-decoration:none;">
        <v-btn
          id="rsv-button"
          :ripple="false"
          color="#002448"
          :disabled="!isChecked"
        >
          <span style="color:white;">예약하기</span>
        </v-btn>
      </router-link>
    </div>
  </div>
</div>
</template>
<script>
export default {
  props: {
    RsvDate: String,
    RsvTable: String
  },
  components: {},
  data() {
    return {
      colors: {
        1: '#d9d9d9',
        2: '#d9d9d9',
        3: '#d9d9d9',
        4: '#d9d9d9',
        5: '#d9d9d9',
        6: '#d9d9d9',
        7: '#d9d9d9',
        8: '#d9d9d9',
        9: '#d9d9d9',
        10: '#d9d9d9',
        11: '#d9d9d9',
        12: '#d9d9d9',
        13: '#d9d9d9',
        14: '#d9d9d9',
        15: '#d9d9d9',
        16: '#d9d9d9',
        17: '#d9d9d9',
        18: '#d9d9d9',
        19: '#d9d9d9',
        20: '#d9d9d9',
        21: '#d9d9d9',
        22: '#d9d9d9',
        23: '#d9d9d9'
      },
      count: 0,
      start_time: '00',
      end_time: '00',
      display_end_time: '00',
      selected: '',
      isChecked: false
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    blue(i) {
      this.colors[i] = '#769fcd'
    },
    gray(i) {
      this.colors[i] = '#d9d9d9'
    },
    setStartTime(i) { // 시작시각 설정
      this.start_time = i
    },
    setEndTime(i) { // 종료시각 설정 및 화면에 표시되는 종료시각 설정
      this.end_time = i
      this.display_end_time = Number(this.end_time) + 1 // 클릭은 버튼 14를 클릭하지만 종료시각은 15시00분이기 때문에 + 1 해줌
    },
    pickTime(i) {
      this.count += 1 // click 하면 count + 1
      if (this.count % 2 === 1) { // count가 홀수면
        this.setStartTime(i) // 시작시각을 클릭한 시각으로 설정하고
        for (let j = 1; j <= 23; j++) { // 클릭한 시각 이외는 전부 회색으로 해라
          this.gray(j)
        }
        this.blue(this.start_time) // 클릭한 시각은 파란색으로 해라
      } else { // count가 짝수면
        if (i < this.start_time) { // 근데 만약 클릭한 시각이 기존에 정해졌던 시작시각보다 이전의 시각이면
          this.count = this.count - 1 // count - 1
          this.gray(this.start_time) // 기존에 선택한 시작시각은 회색으로 하고
          this.setStartTime(i) // 클릭한 시각으로 시작시각을 새롭게 설정해라
          this.blue(this.start_time) // 그리고 클릭한 시각은 파란색으로 해라
        } else { // 클릭한 시각이 기존에 정해졌던 시작시각보다 이후의 시각이면
          this.setEndTime(i) // 그 시각을 종료시각으로 설정해라
          for (let j = this.start_time; j <= this.end_time; j++) { // 그리고 시작시각부터 종료시각까지 전부 파란색으로 해라
            this.blue(j)
          }
        }
      }
    }
  }
}
</script>
<style scoped>
.main-rsv-contents {
  max-width: 900px;
  width: 70%;
  margin: auto;
  margin-top: 48px;
  min-width: 470px;
  padding: 12px;
}
.timeLists {
  display: flex;
  padding: 0px;
  height: 80px;
  margin-bottom: 24px;
}
ul {
  border: 1px solid black;
  border-radius: 5px;
}
li {
  width: 100%;
  height: 100%;
  list-style: none;
  border-right: 1px solid rgb(117, 117, 117);
}
.timeLists > li:last-child {
  border: none;
}
.timeLists > li:last-child > .timetable {
  border-radius: 0px 4px 4px 0px;
}
.timeLists > li:first-child > .timetable {
  border-radius: 4px 0px 0px 4px;
}
.timeLists > li > .timetable {
  width: 100%;
  height: 100%;
  min-width: 10px;
  padding: 0px;
  border-radius: 0;
}
.datecontents {
  display: flex;
  flex-direction: column;
}
.input-title {
  padding-left: 10px;
  color: #658ef8;
  font-size: 13px;
}
.input-text-readonly {
  background-color: #efefef;
}
input, select {
  border: 1px solid #658ef8;
  border-radius: 10px;
  text-align: center;
  width: 100%;
  height: 50px;
  font-size: 20px;
  outline: none;
}
textarea {
  border: 1px solid #658ef8;
  border-radius: 10px;
  width: 100%;
  height: 80px;
  font-size: 20px;
  padding: 10px;
  outline: none;
}
select {
  -webkit-appearance: menulist !important;
  -moze-appearance: menulist !important;
  appearance: menulist !important;
  padding-left: 10px;
}
.content-box {
  display: flex;
  flex-direction: column;
  width: 46%;
  margin-bottom: 19px;
}
.contents-row-last {
  display: flex;
  flex-direction: column;
  width: 100%;
  margin-bottom: 24px;
}
option {
  font-size: 24px;
}
.contents-row {
  display: flex;
  justify-content: space-between;
}
.text-orangered {
  color: orangered;
}
.notice-contents > p {
  margin-top: 3px;
}
.confirm-note {
  text-align: center;
  display: flex;
  justify-content: center;
  margin: 36px 0px;
  line-height: 100%;
}
.confirm-note-checkbox {
  width: 24px;
  height: 24px;
  margin: 4px 8px 4px 0px;
}
.confirm-note-text {
  line-height:32px;
  font-size:24px;
}
.rsv-button {
  margin-bottom: 48px;
}
#rsv-button {
  width: 100%;
  height: 70px;
  font-size: 24px;
}
</style>
