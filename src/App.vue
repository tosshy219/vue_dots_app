<template>
  <div id="app">
    <div class="dotsWrapper">
      <div v-for="(n,index) in sources" :key="n.id" class="dot" :style="afterSources[index]"></div>
    </div>
    <div class="btnWrapper">
      <p class="btn2" v-if="see">{{sources.length}}</p>
      <p class="btn2" v-else @click="confirm()">答え</p>
      <p class="btn" @click="plus()">NEXT!</p>
    </div>
    <p>{{basedStyle}}</p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      number: "",
      sources: [],
      afterSources: [],
      see: false
    };
  },
  computed: {
    basedStyle() {
      return this.sources.forEach(e => {
        const j = "left:" + e + "%";
        this.afterSources.push(j);
      });
    }
  },
  methods: {
    plus() {
      this.sources = [];
      console.log(this.setNum());
      console.log(this.makeRandom());
      this.allChange();
    },

    setNum() {
      const j = Math.floor(Math.random() * 10 + 1);
      this.number = j;
      return j;
    },
    makeRandom() {
      for (let i = -5; i < this.number; i++) {
        const j = Math.random() * 92;
        this.sources.push(j);
      }
      return this.sources;
    },
    confirm() {
      this.see = true;
    },
    allChange() {
      const dots = document.querySelectorAll(".dot");

      dots.forEach((e, index) => {
        e.style.left = this.sources[index] + "%";
      });
      this.see = false;
    }
  },

  created() {
    // 関数はconsole.logに入れても発動するらしい
    console.log(this.setNum());
    console.log(this.makeRandom());
    console.log(this.afterSources);
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  user-select: none;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding-top: 5px;
  color: #2c3e50;
}
.dotsWrapper {
  width: 600px;
  height: 600px;
  margin: 0 auto;
  background-color: bisque;
  border-radius: 10px;
}
.dot {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  position: relative;
  background-color: tomato;
}
.btnWrapper {
  display: flex;
  width: 350px;
  height: 80px;
  margin: 0 auto;
  margin-top: 30px;
  justify-content: space-between;
}

.btn {
  width: 120px;
  height: 50px;
  background-color: coral;
  border-radius: 10px;
  color: white;
  font-size: 40px;
  padding: 10px;
  line-height: 55px;
  box-shadow: 0 2px 0 chocolate;
  text-decoration: none;
  display: block;
}
.btn:hover {
  opacity: 0.6;
  cursor: pointer;
}
.btn2 {
  width: 120px;
  height: 50px;
  background-color: coral;
  border-radius: 10px;
  color: white;
  font-size: 40px;
  padding: 10px;
  line-height: 55px;
  box-shadow: 0 2px 0 chocolate;
  text-decoration: none;
  display: block;
}
.btn2:hover {
  opacity: 0.6;
  cursor: pointer;
}
.btn:active {
  box-shadow: none;
  position: relative;
  top: 2px;
}
@media screen and (max-width: 620px) {
  .dotsWrapper {
    width: 300px;
    height: 300px;
    margin-top: 5px;
    border-radius: 10px;
  }
  .btnWrapper {
    width: 200px;
    height: 150px;
    margin-top: 20px;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
  }
  .btn {
    font-size: 30px;
    height: 30px;
    line-height: 35px;
    width: 80px;
    padding: 15px 30px;
  }
  .btn2 {
    width: 70px;
    height: 30px;
    padding: 15px;
    line-height: 35px;
    font-size: 30px;
  }
  .dot {
    width: 20px;
    height: 20px;
  }
}
</style>
