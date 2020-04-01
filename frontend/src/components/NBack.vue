<template>
  <div>
    <h1>This is NBack</h1>
    <p>{{ randomSequence }}</p>
    <!-- <p>{{ keydownSpaceSequence }}</p> -->
    <!-- <button @click="getRandom">getRandom</button> -->
    <button @click="commence" :disabled="!terminated">Commence</button>
    <button @click="terminate" :disabled="terminated">Terminate</button>
    <p>{{ random }}</p>
  </div>
</template>

<script>
export default {
  name: "NBack",
  // data: local variables
  data() {
    return {
      terminated: true,
      randomSequence: [1, 2, 3, 3, 4, 5],
      currentIndex: 0,
      random: null,
      // interval: null, // setInterval function
      keydownSpace: false,
      keydownSpaceSequence: [false, false, false, false, false, false]
    };
  },
  // mounted, what will do when mounted the page
  mounted() {
    // this.initializeRandomSequence();
    let vm = this;
    window.addEventListener("keydown", function(e) {
      // 32 is the code for space
      if (e.keyCode == 32 && !this.keydownSpace) {
        // console.log(e.keyCode);
        // this.keydownSpace = true;

        let keydownSpaceSequence = vm.keydownSpaceSequence;
        let currentIndex = vm.currentIndex;
        keydownSpaceSequence[currentIndex] = true;
        console.log(vm.keydownSpaceSequence);
        // console.log(currentIndex);
      }
    });
    // setInterval(()=>{
    //   // if () {return}  // terminating condition
    //     this.getRandom()
    // }, 1500),
  },
  // methods: useful functions used here
  methods: {
    initializeRandomSequence() {
      console.log("initializeRandomSequence");
      let numberOfElement = 11;
      for (let i = 0; i < numberOfElement; i++) {
        let randomElement = Math.floor(Math.random() * 10);
        this.randomSequence.push(randomElement);
      }
    },
    getRandom() {
      // console.log("getRandom");
      let currentIndex = this.currentIndex;
      let randomSequence = this.randomSequence;
      let len = randomSequence.length;
      if (currentIndex >= len - 1) {
        this.terminate();
      }
      this.random = this.randomSequence[currentIndex];
      this.currentIndex = currentIndex + 1;
      setTimeout(() => {
        this.random = null;
      }, 1000);
    },
    // keydownSpace(){
    //   console.log("keydown space")
    // },
    commence() {
      this.terminated = false;
      this.currentIndex = 0;
      this.interval = setInterval(() => {
        // if () {return}  // terminating condition
        // this.keydownSpace = false;
        this.getRandom();
      }, 1500);
    },
    terminate() {
      this.terminated = true;
      clearInterval(this.interval);
    }
  },

  // sockets, for talk with backedn
  sockets: {}
};
</script>

<style lang="scss" scoped></style>
