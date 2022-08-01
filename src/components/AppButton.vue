<template>
  <button class='cursor-p' :class="className" @click="this.$emit('app-btn-click')"><slot/></button>
</template>

<script>
export default {
  props:['text','className'],
  emits:['app-btn-click']
}
</script>

<style scoped>

button{
  border: none;
  border-radius: 8px;
  font-size: 14px;
  line-height: 20px;
  padding: 7px 16px;
}
.primary{
  background: #00704B;
  color: #FFFFFF;
}

.secondary{
  background: #F2F2F2;
  color: #737D8A;
}

.danger{
  background: #EC5F5F;
  color: #ffffff;
}

</style>
