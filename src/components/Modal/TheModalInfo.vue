<template>
  <div class="modal-mask">
    <div class="modal-wrapper">
      <div class="modal-container modal-info">

        <div class="flex-jc-end">
          <img class="cursor-p" src="../../assets/img/close.svg" @click="this.$emit('close')"/>
        </div>

        <h1 class="modal-header mb-24">{{ item.name }}</h1>

        <div class="flex-jc-sb mb-24">
          <div class="flex-jc-sb info-group">
            <div class="img-span">
              <img class="cursor-p weight-img" src="../../assets/img/weight.svg"/>
              <span class="small">350 г.</span>
            </div>
            <div class="img-span">
              <img class="cursor-p size-img" src="../../assets/img/diam.svg"/>
              <span class="small">{{ item.size }}</span>
            </div>
          </div>
          <span class="active-sell">{{ item.price }}</span>
        </div>

        <div class="mb-24">
          <div class="flex-jc-sb regular light-grey mb-10">
            <span>Огрурцы</span>
            <div>
              <span class="dark-grey">{{ item.cucumber ? item.cucumber : 'Соленые'  }}</span>
              <span> (10 пупырок)</span>
            </div>
          </div>
          <div class="flex-jc-sb regular light-grey mb-10">
            <span>Острая</span>
            <span class="dark-grey">{{ item.spicy ? 'Да' : 'Нет' }}</span>

          </div>
          <div class="flex-jc-sb regular light-grey">
            <span>Тесто</span>
            <span class="dark-grey">{{ item.thickness }}</span>
          </div>
        </div>

        <p class="regular light-grey">item.comment</p>


      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['item', 'id'],
  emits: ['close'],
}
</script>

<style scoped>

.mb-24 {
  margin-bottom: 24px
}

.mb-10 {
  margin-bottom: 10px
}

.modal-info {
  width: 504px;
  height: 280px;
}

.info-group {
  width: 150px;
}

.img-span {
  display: flex;
  width: 65px;
  justify-content: space-around;
}

.weight-img {
  width: 15px;
}

.size-img {
  width: 20px;
}

</style>
