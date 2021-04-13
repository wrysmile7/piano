<template>
  <div class="home">
    <span class="moon"></span>
    <span
      class="star"
      v-for="(item, index) in 100"
      :key="index"
      :style="{
        animationDelay: starDelay() + 's',
        left: starLeft() + 'px',
        top: starTop() + 'px',
      }"
    ></span>
    <div class="piano">
      <p class="title"></p>
      <div class="box">
        <ul class="keys-wrap white-keys">
          <li v-for="item in whiteNotes" :key="item.keyCode">
            <span>{{ item.key }}</span>
          </li>
        </ul>
        <ul class="keys-wrap black-keys black-keys1">
          <li class="bkey" v-for="item in blackNotes[0]" :key="item.keyCode">
            <span>⇧<br />+<br />{{ item.key }}</span>
          </li>
        </ul>
        <ul class="keys-wrap black-keys black-keys2">
          <li class="bkey" v-for="item in blackNotes[1]" :key="item.keyCode">
            <span>⇧<br />+<br />{{ item.key }}</span>
          </li>
        </ul>
        <ul class="keys-wrap black-keys black-keys3">
          <li class="bkey" v-for="item in blackNotes[2]" :key="item.keyCode">
            <span>⇧<br />+<br />{{ item.key }}</span>
          </li>
        </ul>
        <ul class="keys-wrap black-keys black-keys4">
          <li class="bkey" v-for="item in blackNotes[3]" :key="item.keyCode">
            <span>⇧<br />+<br />{{ item.key }}</span>
          </li>
        </ul>
        <ul class="keys-wrap black-keys black-keys5">
          <li class="bkey" v-for="item in blackNotes[4]" :key="item.keyCode">
            <span>⇧<br />+<br />{{ item.key }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { whiteNotes, blackNotes } from '@/utils/notes'

export default {
  name: 'Home',
  data () {
    return {
      whiteKeys: [1, 2, 3, 4, 5, 6, 7],
      whiteNotes: whiteNotes,
      blackNotes: [[], [], [], [], []],
      homeWidth: 0,
      homeHeight: 0
    }
  },
  components: {
  },
  created () {
    blackNotes.map(val => {
      if (val.id >= 36 && val.id <= 40) {
        this.blackNotes[0].push(val)
      }
      if (val.id >= 41 && val.id <= 45) {
        this.blackNotes[1].push(val)
      }
      if (val.id >= 46 && val.id <= 50) {
        this.blackNotes[2].push(val)
      }
      if (val.id >= 51 && val.id <= 55) {
        this.blackNotes[3].push(val)
      }
      if (val.id >= 56 && val.id <= 60) {
        this.blackNotes[4].push(val)
      }
    })
    console.log(this.blackNotes)
  },
  mounted () {
    this.homeWidth = document.getElementsByClassName('home')[0].clientWidth
    this.homeHeight = document.getElementsByClassName('home')[0].clientHeight
  },
  methods: {
    starDelay () {
      return (Math.random() * 10).toFixed(0)
    },
    starTop () {
      return (Math.random() * this.homeHeight).toFixed(0)
    },
    starLeft () {
      return (Math.random() * this.homeWidth).toFixed(0)
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  font-size: 14px;
  // background: rgba($color: #000000, $alpha: 0.7);
  background-image: linear-gradient(
    180deg,
    #1b2947,
    #2b3152,
    #3b385d,
    #4c4067,
    #5d4771
  );
  display: flex;
  justify-content: center;
  position: relative;
  .moon {
    width: 60px;
    height: 60px;
    position: absolute;
    top: 20px;
    right: 20px;
    border-radius: 50%;
    background: #ecd68c;
    box-shadow: 0 0 20px #ecd68c;
  }
  .star {
    position: absolute;
    width: 0;
    height: 0;
    border: 3px solid transparent;
    border-bottom: 5px solid #fff;
    opacity: 0.3;
    animation: blingbling 3s linear infinite;
    z-index: 0;
    &::before {
      content: "";
      position: absolute;
      top: 4px;
      left: -3px;
      border: 3px solid transparent;
      border-top: 5px solid #fff;
    }
  }
  .piano {
    position: relative;
    z-index: 1;
    height: 400px;
    margin: auto;
    margin-top: 100px;
    display: flex;
    flex-direction: column;
    .title {
      height: 15%;
      background: #000000;
      border-top-left-radius: 5px;
      border-top-right-radius: 5px;
      border-bottom: 2px solid #ccc;
    }
    .box {
      flex: 1;
      position: relative;
      .keys-wrap {
        height: 100%;
        li {
          border-bottom-left-radius: 5px;
          border-bottom-right-radius: 5px;
          display: flex;
          align-items: flex-end;
          justify-content: center;
          padding-bottom: 10px;
          cursor: pointer;
        }
      }
      .white-keys {
        li {
          width: 40px;
          height: 100%;
          background: #fff;
          float: left;
          border: 1px solid #ccc;
          &:hover {
            height: 99%;
          }
        }
      }
      .black-keys {
        width: 280px;
        height: 60%;
        position: absolute;
        top: 0;
        li {
          width: 30px;
          height: 100%;
          background: #000;
          color: #fff;
          float: left;
          position: absolute;
          &:nth-child(1) {
            left: 9%;
          }
          &:nth-child(2) {
            left: 23.5%;
          }
          &:nth-child(3) {
            left: 51.5%;
          }
          &:nth-child(4) {
            left: 66%;
          }
          &:nth-child(5) {
            left: 80.5%;
          }
        }
      }
      .black-keys1 {
        left: 0%;
      }
      .black-keys2 {
        left: 19.5%;
      }
      .black-keys3 {
        left: 39%;
      }
      .black-keys4 {
        left: 58.3%;
      }
      .black-keys5 {
        left: 77.7%;
      }
    }
  }
}
@keyframes blingbling {
  0% {
    opacity: 0.3;
  }
  50% {
    opacity: 0.8;
  }
  100% {
    opacity: 0.3;
  }
}
</style>
