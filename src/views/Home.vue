<template>
  <div class="home">
    <!-- <dv-full-screen-container> -->
		<div class="clock">
    		<p class="time">{{ time }}</p>
		</div>
		<div class="clock" id="date">
			<p class="date">{{ date }}</p>
		</div>
    <dv-border-box-11 title="可视化监控大屏">
      <div class="data_vivew_left">
		  <div class="DataVL_Top">
			  <dv-border-box-7>dv-border-box-7</dv-border-box-7>
		  </div>
	  </div>
    </dv-border-box-11>
    <!-- </dv-full-screen-container> -->
  </div>
</template>

<script>
export default {
  name: "Home",
  data(){
	  return{
		  date:"",
		  time:"",
		  week:['SUN', 'MON', 'TUE', 'WED', 'THU', 'FRI', 'SAT'],
	  }
  },
  created(){
	  setInterval(()=>{
		  this.updateTime()
	  },1000)
  },
  updated(){
	  console.log(11)
	  setInterval(()=>{
		  this.updateTime()
	  },1000)
  },
  methods:{
	  updateTime() {
		var cd = new Date();
		this.time = this.zeroPadding(cd.getHours(), 2) + ':' + this.zeroPadding(cd.getMinutes(), 2) + ':' + this.zeroPadding(cd.getSeconds(), 2);
		this.date = this.zeroPadding(cd.getFullYear(), 4) + '-' + this.zeroPadding(cd.getMonth()+1, 2) + '-' + this.zeroPadding(cd.getDate(), 2) + ' ' + this.week[cd.getDay()];
	  },
	   zeroPadding(num, digit) {
			var zero = '';
			for(var i = 0; i < digit; i++) {
				zero += '0';
			}
			return (zero + num).slice(-digit);
		}
  }
};
</script>
<style lang="less" scoped>
.data_vivew_left {
  width: 25%;
  height: 100vh;
  box-sizing: border-box;
  padding: 50px 30px;
  .DataVL_Top{
	  width: 100%;
	  height: 30vh;
  }
}
.home {
  width: 100%;
  height: 100vh;
  background-image: url("../images/back.png");
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.Flex {
  display: flex;
}
.clock {
  font-family: 'Share Tech Mono', monospace;
  color: #ffffff;
  text-align: center;
  min-width: 150px;
  position: absolute;
  right: 0;
  top: 15px;
  -webkit-transform: translate(-50%, -50%);
          transform: translate(-50%, -50%);
  color: #daf6ff;
  text-shadow: 0 0 20px #0aafe6, 0 0 20px rgba(10, 175, 230, 0);
}
.clock .time {
  letter-spacing: 0.05em;
  font-size: 20px;
  padding: 5px 0;
}
.clock .date {
  letter-spacing: 0.1em;
  font-size: 16px;
}
.clock .text {
  letter-spacing: 0.1em;
  font-size: 12px;
//   padding: 20px 0 0;
}
#date{
	right: 150px;
}
</style>
