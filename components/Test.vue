<template>
  <!--    图片滑块组件-->
  <div class="moveChunk">
    <div class="margin" :style="{padding: imgss[5]}">
      <div class="marginBox">
        <!-- <v-skeleton-loader
          type="image"
          v-if="skeletonVisible"
        ></v-skeleton-loader> -->
        <div
        class="relative"
        ref="imgs"
        @mousedown.prevent="downs"
        @mousemove.prevent="moves"
      >
          <div class="posi" :style="{ width: ws+'%' }">
        <img class="lazyload originImg" :src="img0" :alt="imgss[2]"/>
      </div>
      <img class="lazyload clearImg" :src="img1" :alt="imgss[2]"/>
          <div class="move cu" :style="{ left: ws+'%' }">
            <!-- <img
              src="https://d38b044pevnwc9.cloudfront.net/site/en/assets/image/moveW.png"
              alt="move"
            /> -->
            <!-- <div class="compare">
              <div class="left">Before</div>
              <div class="right">After</div>
            </div> -->
          </div>
        </div>
      <div v-if="imgss.length > 2">
        <a
          :href="imgss[4] ? localePath(imgss[4]) : 'javascript:;'"
          :alt="imgss[2]"
          :style="{ cursor: imgss[4] ? 'pointer' : 'default' }"
        >
          <p class="chunkTitle">{{ imgss[2] }}</p>
          <p class="chunkDescription">{{ imgss[3] }}</p>
        </a>
      </div>
      </div>
    </div>
  </div>
</template>

<script>
// import img1 from '../../assets/clear/1.jpg';
// import img1_1 from '../../assets/clear/1-1.jpg';
import img2 from '../assets/clear/2.jpg';
import img2_2 from '../assets/clear/2-1.jpg';
// import img3 from '../../assets/clear/3.jpg';
// import img3_3 from '../../assets/clear/3-1.jpg';
// import img4 from '../../assets/clear/4.jpg';
// import img4_4 from '../../assets/clear/4-1.jpg';
// import img5 from '../../assets/clear/5.jpg';
// import img5_5 from '../../assets/clear/5-1.jpg';
// import img6 from '../../assets/clear/6.jpg';
// import img6_6 from '../../assets/clear/6-1.jpg';
// import img7 from '../../assets/clear/7.jpg';
// import img7_7 from '../../assets/clear/7-1.jpg';
// import img8 from '../../assets/clear/8.jpg';
// import img8_8 from '../../assets/clear/8-1.jpg';
// import img9 from '../../assets/clear/9.jpg';
// import img9_9 from '../../assets/clear/9-1.jpg';
// import img10 from '../../assets/clear/10.jpg';
// import img10_10 from '../../assets/clear/10-1.jpg';
// import img11 from '../../assets/clear/11.jpg';
// import img11_11 from '../../assets/clear/11-1.jpg';
// import img12 from '../../assets/clear/12.jpg';
// import img12_12 from '../../assets/clear/12-1.jpg';
// import img13 from '../../assets/clear/13.jpg';
// import img13_13 from '../../assets/clear/13-1.jpg';
// import img14 from '../../assets/clear/14.jpg';
// import img14_14 from '../../assets/clear/14-1.jpg';
// import img15 from '../../assets/clear/15.jpg';
// import img15_15 from '../../assets/clear/15-1.jpg';
// import img16 from '../../assets/clear/16.jpg';
// import img16_16 from '../../assets/clear/16-1.jpg';
// import img17 from '../../assets/clear/17.jpg';
// import img17_17 from '../../assets/clear/17-1.jpg';
// import img18 from '../../assets/clear/18.jpg';
// import img18_18 from '../../assets/clear/18-1.jpg';
// import img19 from '../../assets/clear/19.jpg';
// import img19_19 from '../../assets/clear/19-1.jpg';
// import img20 from '../../assets/clear/20.jpg';
// import img20_20 from '../../assets/clear/20-1.jpg';
// import img21 from '../../assets/clear/21.jpg';
// import img21_21 from '../../assets/clear/21-1.jpg';
// import img22 from '../../assets/clear/22.jpg';
// import img22_22 from '../../assets/clear/22-1.jpg';
// import img23 from '../../assets/clear/23.jpg';
// import img23_23 from '../../assets/clear/23-1.jpg';
// import img24 from '../../assets/clear/24.jpg';
// import img24_24 from '../../assets/clear/24-1.jpg';
// import img25 from '../../assets/clear/25.jpg';
// import img25_25 from '../../assets/clear/25-1.jpg';
// import img26 from '../../assets/clear/26.jpg';
// import img26_26 from '../../assets/clear/26-1.jpg';
// import img27 from '../../assets/clear/27.jpg';
// import img27_27 from '../../assets/clear/27-1.jpg';
// import img28 from '../../assets/clear/28.jpg';
// import img28_28 from '../../assets/clear/28-1.jpg';
// import img29 from '../../assets/clear/29.jpg';
// import img29_29 from '../../assets/clear/29-1.jpg';
// import img30 from '../../assets/clear/30.jpg';
// import img30_30 from '../../assets/clear/30-1.jpg';
// import img31 from '../../assets/clear/31.jpg';
// import img31_31 from '../../assets/clear/31-1.jpg';
// import img32 from '../../assets/clear/32.jpg';
// import img32_32 from '../../assets/clear/32-1.jpg';
// import img33 from '../../assets/clear/33.jpg';
// import img33_33 from '../../assets/clear/33-1.jpg';
// import img34 from '../../assets/clear/34.jpg';
// import img34_34 from '../../assets/clear/34-1.jpg';
// import img35 from '../../assets/clear/35.jpg';
// import img35_35 from '../../assets/clear/35-1.jpg';
// import img36 from '../../assets/clear/36.jpg';
// import img36_36 from '../../assets/clear/36-1.jpg';
// import img37 from '../../assets/clear/37.jpg';
// import img37_37 from '../../assets/clear/37-1.jpg';

export default {
  name: "index",
  props: {
    imgss: { type: Array }
  },
  data() {
    return {
      openMoves: false,
      ws: 100,
      skeletonVisible: true,
      img0: '',
      img1: '',
      i: 1
    };
  },
  methods: {
    downs(e) {
      this.openMoves = true;
      this.moves(e);
    },
    moves(e) {
      // e.preventDefault()
      if (!this.openMoves) return;
      let cBoxW = this.$refs.imgs.getBoundingClientRect().left; //对比offset 的方向值需要考虑到父级，如果父级是定位元素，那么子元素的offset值相对于父元素，如果父元素不是定位元素，那么子元素的offset值相对于 可视区窗口。getBoundingClientRect() 的值只相对于可视去窗口。
      let l = e.clientX - cBoxW;
      if (l >= this.$refs.imgs.offsetWidth) this.ws = "100%";
      else if (l < 0) this.ws = 0;
      else this.ws = (l / this.$refs.imgs.offsetWidth) * 100 + "%";
    },
    ups(e) {
      this.openMoves = false;
    },
    getImgWidth() {
      let oImg = new Image();
      oImg.crossOrigin = "";
      oImg.src = this.imgss[1];
      oImg.onload = () => {
        this.skeletonVisible = false;
      };
    }
  },
  mounted() {
    window.addEventListener("mouseup", this.ups);
    // this.getImgWidth();
    this.img0 = img2
    this.img1 = img2_2
    let timer = setInterval(() => {
      // if(this.i >= 100) clearInterval(timer)
      // console.log(this.ws);
      if(this.ws <= 0) {
        this.ws = 100
      }
      // if(this.ws < 10) {
      //   this.ws -= 1
      // }else {
      //   this.ws -= this.ws/20
      // }
      this.ws -= 0.2
      this.i++
    }, 0.002)
  }
};
</script>

<style scoped lang="scss">
.moveChunk {
  .margin {
    // max-width: 75rem;
    margin: 0 auto;
    padding: 0 .75rem;
    margin-bottom: 1.875rem;
  }
  .marginBox {
    max-width: 960px;
    margin: 0 auto;
  }
  .relative {
    position: relative;
    margin-bottom: 1.4375rem;
    line-height: 0;
    text-align: left;
    // border-radius: 0.75rem;
    .clearImg {
      width: 100%;
      // border-radius: 0.75rem;
    }
    .originImg {
      height: 100%;
    }
    .posi {
      position: absolute;
      left: 0;
      top: 0;
      width: 50%;
      height: 100%;
      overflow: hidden;
      // border-radius: 0.75rem 0 0 0.75rem;
    }
    .move {
      position: absolute;
      height: 100%;
      top: 0;
      left: 0%;
      transform: translateX(-50%);

      border-left: 12px solid #fff;
      img {
        height: 100%;
      }
      .compare {
        display: flex;
        border-radius: 20px;
        background-color: rgba($color: #000000, $alpha: 0.5);
        position: absolute;
        left: 50%;
        top: 25%;
        transform: translateX(-50%);
        z-index: -1;
        .left, .right {
          width: 70px;
          padding: 20px 0;
          text-align: center;
          color: #fff;
        }
      }
    }
    .move:hover {
      cursor: ew-resize;
    }
  }
  .chunkTitle {
    line-height: 1;
    font-size: 1.125rem;
    color: #000;
    margin-bottom: 0.5625rem;
    text-align: left;
    font-weight: bold;
  }
  .chunkDescription {
    font-size: 0.75rem;
    color: #666;
    text-align: left;
  }
  a {
    text-decoration: none;
  }
}
</style>
