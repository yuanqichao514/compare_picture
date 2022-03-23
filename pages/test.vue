<template>
  <div class="test">
    <move-chunk :imgss="chunk"/>
  </div>
</template>

<script>
import MoveChunk from '@/components/Test.vue';

  export default {
    name: 'test',
    components: {
      MoveChunk
    },
    data () {
      return {
        chunk: ["", "",  "", "", "", "0 2.5rem"],
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .test {
    padding-top: 100px;
  }
</style>