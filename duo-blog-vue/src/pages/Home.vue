<!-- 首页 -->
<template>
  <div>
    <sg-navbar></sg-navbar>
    <div class="container">
      <el-row  :gutter="30">
        <el-col :sm="24" :md="16" style="transition:all .5s ease-out;margin-bottom:30px;">
          <sg-articlelist></sg-articlelist>
        </el-col>
        <el-col :sm="24"  :md="8" >
          <sg-rightlist></sg-rightlist>
        </el-col>
      </el-row>
      <div class="shell">
        <div class="item1"></div>
        <div class="item1"></div>
      </div>
    </div>
    <!-- <img class="image" :src="url" alt="" :style="{left: '100px', top: '100px'}"> -->
  </div>
</template>

<script>
import header from '../components/header.vue'
import articlelist from '../components/articlelist.vue'
import rightlist from '../components/rightlist.vue'
export default {
  name:'Home',
  data() { //选项 / 数据
    return {
      url: '../../static/img/favicon copy.ico'
    }
  },
  methods: { //事件处理器

  },
  components: { //定义组件
    'sg-navbar':header,
    'sg-articlelist':articlelist,
    'sg-rightlist':rightlist,
  },
  created() { //生命周期函数

  }
}
// var pic = document.getElementsByClassName('image');
// document.addEventListener( 'mousemove',function(e) {
//     var x = e.pageX;
//     var y = e.pageY;
//     console.log('x坐标是'+ x,'y坐标是' + y);
//     pic.style.left = x - 50 + 'px';
//     pic.style.top = y - 40 + 'px';
// });
var flag = true //节流阀
document.addEventListener('mousemove', function (e) {
  if (flag) {
    flag = false  //关闭

    var item =Array.from(document.querySelectorAll('.item1'))
    //获取鼠标位置
    var mouseX = e.clientX
    var mouseY = e.clientY;
    item.forEach(function (sqr, index) {
      //获取元素位置
      var sqrX = sqr.offsetLeft;
      var sqrY = sqr.offsetTop;
      //鼠标位置减去元素位置获取当前元素坐标
      var diffX = mouseX - sqrX
      var diffY = mouseY - sqrY
      //Math.atan2(y,x) 返回x轴到(x,y)的角度 //pi值
      var radians = Math.atan2(diffY, diffX)

      var angle = radians * 180 / Math.PI //角度
      sqr.style.transform = `rotate(${angle}deg)`
    });
    setTimeout(function () {
      flag = true  //打开
    }, 30)
  }
})
</script>

<style>
.image{
  position: absolute;
  top: 100px;
  width: 50px;
  height: 50px;
  left: 100px;
}
.shell {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 1500px;
  height: 100px;
  display: grid;
  grid-template-columns: repeat(6, 50px);
  grid-template-rows: repeat(6, 50px);
  grid-gap: 2rem;
}

.item1 {
  width: 50px;
  height: 50px;
  background-color: rgb(40, 40, 40);
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  border-left: solid 10px #fff;
  position: relative;
}

.item1::after,
.item1::before {
  content: "";
  width: 5px;
  height: 5px;
  position: absolute;
  border-radius: 50%;
  background-color: skyblue;
  left: 30px;
}

.item1::after {
  top: 15px;
}

.item1::before {
  bottom: 15px;
}
</style>
