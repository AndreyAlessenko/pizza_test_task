<template>

<!--  <div class="modal">-->
<!--    <div class='modalBody'>modal</div>-->
<!--  </div>-->


    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="putToEnd">
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

/*.modal{*/
/*  position: absolute;*/
/*  top: 0;*/
/*  bottom: 0;*/
/*  right: 0;*/
/*  left: 0;*/
/*  background: #6c6c6c;*/
/*  opacity: 0.5;*/
/*  display: flex;*/
/*  align-items: center;*/
/*  justify-content: center;*/
/*  z-index: 10;*/

/*}*/


/*.modalBody {*/
/*  opacity: 1;*/
/*  width: 100px;*/
/*  height: 100px;*/
/*  border: 1px solid black;*/
/*  color: black;*/
/*  background: #FFFFFF;*/
/*}*/

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 531px;
  height: 144px;
  margin: 0 auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.putToEnd{
  display: flex;
  justify-content: end;
}

.putToBottom{
  margin-top: 55px;
}

</style>
