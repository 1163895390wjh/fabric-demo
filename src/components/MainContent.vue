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
      // interactive: true, //???????????????????????????
      // selection: true, //?????????????????????
      selectionBorderColor: 'rgba(51,102,153,0.85)', //???????????????????????????
      // perPixelTargetFind: true,
    };
    const cav = new fabric.Canvas(canvasInstance.value, options);

    let txt =
      '???????????????jo 9???13???\n' +
      '????????????????????????????????????\n' +
      '?????????-????????800??????????????????????????????????????????\n' +
      '???????????????????????????\n' +
      '??????\n' +
      '?????????????????????1??????92.3??????????????????\n' +
      '????????????\n' +
      '01\n' +
      '?????????????????????????????????????????????????????????\n' +
      '?????????-????????800?????????????????????????????????(???????????????)??????????????????????????????????????????????????????????????????????????????????????????+??????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????\n' +
      '????????????????????????????????????????????????????????????\n' +
      '02\n' +
      '???????????????????????????\n' +
      '?????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????\n' +
      '??????????????????????????????????????????\n' +
      '????????????\n' +
      '01\n' +
      '????????????\n' +
      '????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????\n' +
      '????????????????????????2472?????????????????????????????????682???????????????????????????1635??????????????????13.5???????????????????????????8???????????????9?????????????????????14??????\n' +
      '02\n' +
      '????????????\n' +
      '?????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????2.472??????????????????????????????200???~300???????????????????????????????????????30???/??????????????????15?????????\n' +
      '03\n' +
      '????????????\n' +
      '???????????????????????????4?????????????????????2????????????2?????????????????????????????????168????????????170.2?????????????????????????????????187????????????189.2???????????????????????????48????????????63???????????????????????????51????????????66??????\n' +
      '04\n' +
      '????????????\n' +
      '???????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????\n' +
      '????????????\n' +
      '????????????????????800??????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????5??????????????????????????????2140????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????\n' +
      '?????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????56%???\n' +
      '?????????????????????????????????????????????????????????7??????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????\n' +
      '???????????????????????????\n' +
      '?????????????????????\n' +
      '??????????????????\n' +
      '??????????????????????????????\n' +
      '?????????????????????????????????????????? ??????\n' +
      '\niosfio?????? ??????????????????';
    const text = new fabric.Textbox('', {
      text: txt,
      fontSize: 20,
      textAlign: 'left',
      width: state.realWidth / state.ratio,
      // height: state.realHeight / state.ratio,
      // lineHeight: 1.2,
      // stroke: 'green',
      // textBackgroundColor: 'rgba(0,0,0,0.5)',
      isWrapping: true, //????????????
      // lockScalingFlip: true,

      splitByGrapheme: true, //???????????????
      // direction: 'ltr',

      cursorColor: 'rgb(54,175,236)',
      editable: true, //?????????
      // isEditing: true, //????????????????????????
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
