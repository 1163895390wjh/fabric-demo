<template>
  <div class="box" ref="boxRef">
    <canvas
      id="mainContentRef"
      ref="canvasInstance"
      :width="state.realWidth"
      :height="state.realHeight"
      :style="{ width: state.canvasWidth, height: state.canvasHeight }"
    ></canvas>
  </div>
</template>

<script setup lang="ts">
  import { fabric } from 'fabric';
  import { onMounted, onUnmounted, reactive, ref } from 'vue';
  import { Canvas, ICanvasOptions } from 'fabric/fabric-impl';

  const canvasInstance = ref();
  const boxRef = ref();

  // const getPixelRatio = function (context) {
  //   let backingStore =
  //     context.backingStorePixelRatio ||
  //     context.webkitBackingStorePixelRatio ||
  //     context.mozBackingStorePixelRatio ||
  //     context.msBackingStorePixelRatio ||
  //     context.oBackingStorePixelRatio ||
  //     context.backingStorePixelRatio ||
  //     1;
  //   return (window.devicePixelRatio || 1) / backingStore;
  // };
  type StateType = { realWidth: number; realHeight: number; ratio: number; canvasWidth: number; canvasHeight: number };
  let state = reactive<StateType>({
    realWidth: 0,
    realHeight: 0,
    ratio: 2,
    canvasWidth: 0,
    canvasHeight: 0,
  });
  onMounted(() => {
    // const context = (document.querySelector('canvas') as HTMLCanvasElement).getContext('2d');
    // const ratio = getPixelRatio(context);
    const ratio = window.devicePixelRatio;
    // console.log(ratio);

    console.log(boxRef.value.offsetWidth);
    const realWidth = boxRef.value.offsetWidth - 30;
    const realHeight = boxRef.value.offsetHeight - 30;
    const canvasWidth = realWidth / ratio;
    const canvasHeight = realHeight / ratio;
    state = { realWidth, realHeight, ratio, canvasWidth, canvasHeight };
    console.log(state);
    initData();
  });
  onUnmounted(() => {
    canvasInstance.value.dispose();
  });
  const initData = () => {
    const options: Partial<ICanvasOptions> = {
      enableRetinaScaling: true,
      width: state.realWidth,
      height: state.realHeight,
      backgroundColor: '#fff',
      // allowTouchScrolling: true,
      // interactive: true, //画布是否是交互式的
      // selection: true, //是否启用组选择
      selectionBorderColor: 'rgba(51,102,153,0.85)', //选择元素的边框颜色
      // perPixelTargetFind: true,
    };
    const cav = new fabric.Canvas(canvasInstance.value, options);

    let txt =
      '晶是是是晶jo 9月13日\n' +
      '中国能建山西院勘察设计的\n' +
      '白鹤滩-浙江±800千伏特高压直流输电工程重庆段\n' +
      '顺利完成长江大跨越\n' +
      '至此\n' +
      '白浙线重庆段渝1标段92.3公里线路贯通\n' +
      '项目背景\n' +
      '01\n' +
      '全球首个、世界首次，优势明显、效益显著\n' +
      '白鹤滩-浙江±800千伏特高压直流输电工程(下称白浙线)是全球首个混合级联特高压直流工程，在世界上首次研发“常规直流+柔性直流”的混合级联特高压直流输电技术，集成特高压直流输电大容量、远距离、低损耗，以及柔性直流输电控制灵活、系统支撑能力强的优势，示范引领意义重大。\n' +
      '远眺重庆长江大跨越段，云雾缭绕、美不胜收\n' +
      '02\n' +
      '西电东送、外电入浙\n' +
      '白浙线是落实我国西电东送能源战略的重点工程，可以有力保障白鹤滩水电站大规模电力外送，促进四川资源优势转化为经济优势，助力西部经济崛起。同时，也是一条外电入浙的能源大动脉，对浙江能源领域实现碳达峰碳中和具有重要意义。\n' +
      '落日余晖下的重庆长江大跨越段\n' +
      '技术探秘\n' +
      '01\n' +
      '工程介绍\n' +
      '山西院负责勘察设计的白浙线重庆段江津长江大跨越工程位于重庆市江津区白沙镇，地形起伏大、水系发达，通航等级高，安全要求高。\n' +
      '工程耐张段长度为2472米，跨越处长江江面宽约682米。铁塔之间跨度达1635米，每轴重达13.5吨，单根线放线张力8吨、牵引力9吨、紧线张力近14吨。\n' +
      '02\n' +
      '地理数据\n' +
      '重庆江津长江大跨越起于重庆市江津区白沙镇团房村开始，止于重庆市江津区白沙镇石孔湾村。线路长度为2.472公里，沿线海拔高度为200米~300米，地形为丘陵。设计风速为30米/秒；设计覆冰15毫米。\n' +
      '03\n' +
      '设计数据\n' +
      '此段线路共使用铁塔4基，其中跨越塔2基，锚塔2基。西岸悬垂跨越塔呼高168米，全高170.2米；东岸悬垂跨越塔呼高187米，全高189.2米；西岸耐张塔呼高48米，全高63米；东岸耐张塔呼高51米，全高66米。\n' +
      '04\n' +
      '设计亮点\n' +
      '杆塔高度越高，设计难度更大，横担端部导、地线挂点去除了构造复杂独立挂架结构，采用横担下平面构造挂点，结构受力更为合理，且杆塔外型更加优美。\n' +
      '项目概况\n' +
      '白鹤滩—浙江±800千伏特高压直流输电工程，起于四川省凉山州的布拖换流站，止于浙江省杭州市的浙北换流站，途经四川、重庆、湖北、安徽、浙江5省（市），线路长度约2140千米，需进行四川宜宾岷江、重庆江津长江、湖北钟祥汉江、安徽池州长江等四处大跨越。\n' +
      '中国能建中电工程所属企业西南院、东北院、山西院、中南院、广东院、江苏院、安徽院、西北院参与完成勘察设计工作，合计里程占整体线路56%。\n' +
      '项目投产后，白鹤滩水电站发出的电只需要7毫秒便可送至浙江，保障华东用电负荷增长需要，同时，将有力保障白鹤滩水电站大规模外送，促进四川资源优势转化为经济优势，推动西部经济发展，助力“双碳”目标实现。\n' +
      '欢迎转载请注明来源\n' +
      '编辑：张任田慧\n' +
      '校审：储信艳\n' +
      '来源：中国能建山西院\n' +
      '中标！一大批新项目集结中··· ···\n' +
      '\niosfio哦搜 埃及模可死哦';
    const text = new fabric.Textbox('', {
      text: txt,
      fontSize: 20,
      textAlign: 'left',
      width: state.realWidth / state.ratio,
      // height: state.realHeight / state.ratio,
      // lineHeight: 1.2,
      // stroke: 'green',
      // textBackgroundColor: 'rgba(0,0,0,0.5)',
      isWrapping: true, //是否换行
      // lockScalingFlip: true,

      splitByGrapheme: true, //中文时设置
      // direction: 'ltr',

      cursorColor: 'rgb(54,175,236)',
      editable: true, //可编辑
      // isEditing: true, //是否处理编辑模式
      // canvas: canvas,
      hasControls: false,

      lockMovementX: true,
      lockMovementY: true,
      lockRotation: true,
      lockScalingX: true,
      lockScalingY: true,
      lockSkewingX: true,
      lockSkewingY: true,
      lockUniScaling: true,
      scaleX: state.ratio,
      scaleY: state.ratio,
    });
    const height = text.calcTextHeight();
    console.log(height);
    text.height = height;
    cav.add(text);

    canvasInstance.value = cav;
  };
  console.log(fabric);
</script>

<style scoped lang="less">
  .box {
    height: 100%;
    width: 100%;
    padding: 15px;
  }
</style>
