<template>
  <div class="home">
    <!-- <dv-loading>Loading...</dv-loading> -->
    <div class="clock">
      <p class="time">{{ time }}</p>
    </div>
    <div class="clock" id="date">
      <p class="date">{{ date }}</p>
    </div>
    <dv-border-box-11 title="可视化监控大屏">
		 
		<div class="Flex">
				<!-- left-top -->
      <div class="data_vivew_left">
        <div class="DataVL_Top">
          <dv-border-box-8 :color="['#5169a7']" :reverse="true">
            <p class="Title">设备监控</p>
            <dv-capsule-chart :config="config" style="width:400px;height:230px;margin:0 auto;" />
          </dv-border-box-8>
        </div>
		<!-- left-top end -->

		<!-- left-center -->
        <div class="DataVL_Center">
          <dv-border-box-8 :color="['#5169a7']" :reverse="true">
            <p class="Title">销量排名</p>
            <dv-scroll-ranking-board
              :config="TopData"
              style="width:400px;height:500px;margin:0 auto;"
            />
          </dv-border-box-8>
        </div>
		<!-- left-center end -->
      </div>
	  <div class="data_vivew_center">
		  <DataVivewCity />
	  </div>
		</div>
    </dv-border-box-11>
  </div>
</template>

<script>
import DataVivewCity from "../components/3Dcity"
export default {
  name: "Home",
  components:{DataVivewCity},
  data() {
    return {
      date: "",
      time: "",
      week: ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"],
      config: {
        data: [
          {
            name: "CPU",
            value: 60
          },
          {
            name: "内存",
            value: 90
          },
          {
            name: "温度",
            value: 37
          },
          {
            name: "网络",
            value: 100
          },
          {
            name: "湿度",
            value: 50
          }
        ],
        unit: ""
      },
      TopData: {
        data: [
          {
            name: "周口",
            value: 55
          },
          {
            name: "南阳",
            value: 120
          },
          {
            name: "西峡",
            value: 78
          },
          {
            name: "驻马店",
            value: 66
          },
          {
            name: "新乡",
            value: 80
          },
          {
            name: "信阳",
            value: 45
          },
          {
            name: "漯河",
            value: 29
          },
          {
            name: "石家庄",
            value: 29
          },
          {
            name: "北京",
            value: 30
          }
        ],
        rowNum: 8
      }
    };
  },
  created() {
    setInterval(() => {
      this.updateTime();
    }, 1000);
  },
  updated() {},
  methods: {
    updateTime() {
      var cd = new Date();
      this.time =
        this.zeroPadding(cd.getHours(), 2) +
        ":" +
        this.zeroPadding(cd.getMinutes(), 2) +
        ":" +
        this.zeroPadding(cd.getSeconds(), 2);
      this.date =
        this.zeroPadding(cd.getFullYear(), 4) +
        "-" +
        this.zeroPadding(cd.getMonth() + 1, 2) +
        "-" +
        this.zeroPadding(cd.getDate(), 2) +
        " " +
        this.week[cd.getDay()];
    },
    zeroPadding(num, digit) {
      var zero = "";
      for (var i = 0; i < digit; i++) {
        zero += "0";
      }
      return (zero + num).slice(-digit);
    }
  }
};
</script>
<style lang="less" scoped>
.data_vivew_center{
	flex: 1;
}
.Title {
  text-align: center;
  color: #fff;
  font-size: 500;
  padding-top: 10px;
  font-size: 20px;
}
.data_vivew_left {
  width: 25%;
  height: 100vh;
  box-sizing: border-box;
  padding: 50px 30px;
  .DataVL_Top {
    width: 100%;
    height: 30vh;
  }
  .DataVL_Center {
    margin-top: 2vh;
    width: 100%;
    height: 60vh;
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
  font-family: "Share Tech Mono", monospace;
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
#date {
  right: 150px;
}
</style>
