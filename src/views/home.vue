<template>
  <div class="normal img-area">
    <div v-if="pon">
      <img v-if="this.bot === 0" src="@/assets/goo.jpg" alt="グー" />
      <img v-if="this.bot === 1" src="@/assets/choki.jpg" alt="チョキ" />
      <img v-if="this.bot === 2" src="@/assets/paa.jpg" alt="パー" />
    </div>
    <div v-else>
      <img class="animation goo" src="@/assets/goo.jpg" alt="グー" />
      <img class="animation choki" src="@/assets/choki.jpg" alt="チョキ" />
      <img class="animation paa" src="@/assets/paa.jpg" alt="パー" />
    </div>
    <div class="button_wrapper">
      <button v-for="item in shapes" :key="item.key" @click="select(item.key)">{{ item.label }}</button>
    </div>
    <div class="ichido_wrapper">
      <button class="ichido" @click="retry">もう一回！</button>
      <p>{{ resultText }}</p>
    </div>
    <div class="syouhai">
      <p>勝ち {{ winCount }}回</p>
      <p>負け {{ loseCount }}回</p>
      <p>あいこ {{ drawCount }}回</p>
    </div>
    <div class="syouritu_wrapper">
      <p>回数 {{ count }}回</p>
      <p>勝率 {{ winRate }}％</p>
    </div>
    <div class="neko1">
      <img src="../assets/neko1.jpg" alt />
    </div>
    <div class="neko2">
      <img src="../assets/neko2.jpg" alt />
    </div>
      <div class="hukidashi">
      <img src="../assets/hukidashi.jpg" alt />
    </div>
  </div>
</template>

<script>
export default {
  name: "janken",
  data: function() {
    return {
      shapes: [
        { label: "ぐー", key: 0 },
        { label: "ちょき", key: 1 },
        { label: "ぱー", key: 2 }
      ],
      count: 0,
      winCount: 0,
      loseCount: 0,
      drawCount: 0,
      resultText: "",
      winRate: 0,
      pon: false
    };
  },
  methods: {
    select(key) {
      if (this.count % 4 === 0) {
        this.player = key;
        this.wazato();
        this.syouritu();
        this.pon = true;
      } else {
        this.player = key;
        this.result();
        this.syouritu();
        this.pon = true;
      }
    },
    result() {
      this.bot = Math.floor(Math.random() * 3);
      switch ((this.player - this.bot + 3) % 3) {
        case 0:
          this.resultText = "あいこー";
          this.drawCount++;
          this.count++;
          break;
        case 1:
          this.resultText = "負け…";
          this.loseCount++;
          this.count++;
          break;
        case 2:
          this.resultText = "勝ち！";
          this.winCount++;
          this.count++;
          break;
      }
    },
    wazato() {
      if (this.player === 0) {
        this.resultText = "勝ち！";
        this.winCount++;
        this.count++;
        this.bot = 1;
      } else if (this.player === 1) {
        this.resultText = "勝ち！";
        this.winCount++;
        this.count++;
        this.bot = 2;
      } else {
        this.resultText = "勝ち！";
        this.winCount++;
        this.count++;
        this.bot = 0;
      }
    },
    syouritu() {
      this.winRate = Math.floor((this.winCount / this.count) * 100);
    },
    retry() {
      this.pon = false;
      this.resultText = "";
      this.player = "";
    }
  }
};
</script>

<style scoped>
.normal {
  height: 520px;
  max-width: 1300px;
  margin: 0 auto;
  padding-top: 40px;
  background-color: #eaf4ff;
}
.normal p {
  font-size: 24px;
}
img {
  width: 220px;
  border-radius: 50%;
}
.syouhai {
  width: 420px;
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
}

.animation {
  animation-name: img;
  animation-duration: 0.3s;
  animation-iteration-count: infinite;
  opacity: 0;
}
@keyframes img {
  0% {
    opacity: 0;
  }
  25% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}
.img-area {
  position: relative;
  margin-bottom: 10px;
}
.animation.choki {
  position: absolute;
  top: 8%;
  left: 42%;
  animation-delay: 0.1s;
}
.animation.paa {
  position: absolute;
  top: 8%;
  left: 42%;
  animation-delay: 0.2s;
}
button {
  border: 3px solid gray;
  margin: 0 20px;
  padding: 0 20px;
  font-size: 32px;
  font-weight: bold;
}
.button_wrapper {
  margin: 24px auto 20px;
}
.syouritu_wrapper {
  width: 300px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
}
.syouritu_wrapper p {
  margin-top: 0;
}
.ichido {
  font-weight: bold;
  color: #2c3e50;
  background-color: #ffffb2;
}
.ichido_wrapper {
  width: 420px;
  margin: 0 auto;
  display: flex;
}
.ichido_wrapper p {
  margin: 0;
  font-size: 34px;
  font-weight: bold;
}
.neko1 {
  width: 220px;
  transform: translate(76%, -436%);
}
.neko2 {
  width: 220px;
  transform: translate(414%, -534%);
}
.hukidashi img {
  width: 100px;
  transform: translate(460%, -1360%);
}
</style>


