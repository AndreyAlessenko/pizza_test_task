<template>

    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container modal-del">

          <div class="flex-jc-end">
            <img class="cursor-p" src="../../assets/img/close.svg" @click="this.$emit('close')"/>
          </div>

          <h1 class="modal-header">Удалить пиццу "{{name}}"</h1>

          <div class="putToEnd putToBottom">
            <app-button
                style="margin-right: 12px"
                :className="'danger'"
                @app-btn-click="this.$emit('confirm-deleting', id)">
              Удалить
            </app-button>
            <app-button
                :className="'secondary'"
                @app-btn-click="this.$emit('close')">
              Отмена
            </app-button>
          </div>

        </div>
      </div>
    </div>

</template>

<script>
import AppButton from '../AppButton'

export default {
  props:['name','id'],
  emits:['close','confirm-deleting'],
  components:{
    AppButton
  }
}
</script>

<style scoped>

.modal-del{
  width: 531px;
  height: 144px;
}

.putToEnd{
  display: flex;
  justify-content: end;
}

.putToBottom{
  margin-top: 55px;
}

</style>
