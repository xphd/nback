<template>
  <div>
    <h1>This is NBack</h1>
    <!-- <button @click="getRandom">getRandom</button> -->
    <p>{{ random }}</p>
  </div>
</template>

<script>
export default {
  name: "NBack",
  // data: local variables
  data() {
    return {
      random: null,
      interval: 1 // time interval in second
    };
  },
  // mounted, what will do when mounted the page
  mounted() {
    setInterval(this.getRandom, 500)
  },
  // methods: useful functions used here
  methods: {
    getRandom() {
      let number = Math.floor(Math.random() * 10);
      this.random = number;
    }
  },

  // sockets, for talk with backedn
  sockets: {}
};
</script>

<style lang="scss" scoped></style>
