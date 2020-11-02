<template>
  <div class="box">
    <div 
      class="box1" 
      v-for="(val, key) in dataList" 
      :key="key" 
      :style="{width: val.width, backgroundColor: val.color}"
    >
    </div>
    <div 
      class="box1" 
      v-for="(val, key) in resArr" 
      :key="key" 
      :style="genStyleStr(val)"
    >
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      dataArr: [7, 14, 121, 23, 5, 92, 56, 78, 28],
      dataList: {},
      dataArr1: [7, 14, 121, 23, 5, 92, 56, 78, 28],
      dataList1: {},
      resArr: [],
      maxVal: null,
    };
  },
  created() {
    this.init();
    this.init1();
  },
  methods: {
    init1() {
      this.resArr = this.dataArr1;
      const arr = this.resArr;
      let max = arr[0];
      for (let i=1;i<arr.length;i++) {
        if (arr[i]>max) {
          max = arr[i];
        }
      }
      this.maxVal = max;
    },
    genStyleStr (val) {
      const max = this.maxVal;
      const perc = val/max;
      const widthStr = 'width:'+(perc*500)+'px;';
      const R = 255*perc;
      const G = 255-R;
      const colorStr = 'background:rgb('+R+','+G+',0)';
      return widthStr + colorStr
    },
    init() {
      let arr = this.dataArr;
      // 找最大和最小数据
      let max = arr[0];
      // 规定最大高度和最小高度
      let maxWidth = 500
      for (let i = 1; i < arr.length; i++) {
        if(arr[i] > max){
          max = arr[i]
        }
      }
      // 遍历数组找颜色和宽度
      // 绿色： #00ff00 [0,255,0]
      // 红色  #ff0000  [255,0,0]
      let currentNum = null
      let currentWidth = null
      let currentR = null
      let currentG = null
      let currentColor = ""
      for(let i = 0; i < arr.length; i++){
        // 设置宽度
        currentNum = arr[i]
        currentWidth = currentNum/max*maxWidth
        this.dataList[i] = {}
        this.dataList[i].width = currentWidth + 'px'
        // 设置颜色
        currentR = currentNum/max*255
        currentG = 255 - currentNum/max*255
        currentColor +="rgb(" + currentR+ "," + currentG + ",0)"
        this.dataList[i].color = currentColor
        currentColor = ""
      }
      console.log(this.dataList)
      // 排序
      this.dataArr1.sort(function(a,b){
        return b - a
      })
      console.log(this.dataArr1)
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
  margin-top: 100px;
  margin-left: 100px;
}
.box1 {
  height: 10px;
  margin-bottom: 10px;
}

</style>
