<template>
  <div>
    <h1>This is NBack</h1>

    <p>{{ randomSequence }}</p>
    <!-- <p>{{ keydownSpaceSequence }}</p> -->
    <!-- <button @click="getRandom">getRandom</button> -->
    <button
      type="button"
      class="btn btn-primary"
      @click="commence"
      :disabled="!terminated"
    >
      Commence
    </button>
    <button
      type="button"
      class="btn btn-danger"
      @click="terminate"
      :disabled="terminated"
    >
      Terminate
    </button>
    <p>
      <font size="100">{{ random }}</font>
    </p>
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
      currentIndex: -1,
      random: null,
      // interval: null, // setInterval function
      keydownSpace: 0, // 0 for false, 1 for true
      keydownSpaceSequence: null //[0, 0, 0, 0, 0, 0] // 0 for false, 1 for true
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
        keydownSpaceSequence[currentIndex] = 1;
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
      currentIndex++; // = currentIndex + 1;
      this.currentIndex = currentIndex;
      if (currentIndex > len - 1) {
        this.terminate();
      }
      this.random = this.randomSequence[currentIndex];

      setTimeout(() => {
        this.random = null;
      }, 1000);
    },
    // keydownSpace(){
    //   console.log("keydown space")
    // },
    commence() {
      this.terminated = false;
      this.currentIndex = -1;
      this.keydownSpaceSequence = [0, 0, 0, 0, 0, 0];
      this.getRandom();
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
