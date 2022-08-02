<template>


  <div class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container modal-create">

        <div class="flex-jc-end">
          <img class="cursor-p" src="../../assets/img/close.svg" @click="this.$emit('close')"/>
        </div>

        <h1 class="modal-header">Создать пиццу</h1>

      </div>
    </div>
  </div>

</template>

<script>
export default {



}
</script>

<style scoped>

.modal-info {
  width: 504px;
  height: 741px;
}

</style>
