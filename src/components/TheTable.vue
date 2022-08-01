<template>
  <div class="grid grid_header">
    <div class="ps-16">#</div>
    <div></div>
    <div class="ps-16">Название</div>
    <div class="ps-16">Огурцы</div>
    <div class="ps-16">Тесто</div>
    <div class="ta-c">Размер</div>
    <div class="ta-c">Острая пицца</div>
    <div class="ta-c">Цена</div>
    <div class="ta-c" >Дата создания шедевра</div>
  </div>

  <div class="grid grid_body">
    <the-table-row v-for="(item,idx) in list"
       :key="idx"
       :item="item"
       @edit-pizza="editPizza"
       @delete-pizza="deletePizza"
       @get-info="getInfo"
    />
  </div>

</template>

<script>
import TheTableRow from '@/components/AppTableRow'
export default {
  props:['list'],
  emits:['edit-pizza', 'delete-pizza','get-info'],
  components:{
    TheTableRow
  },
  methods:{
    editPizza(id){
      this.$emit('edit-pizza', id)
    },
    deletePizza(id){
      this.$emit('delete-pizza', id)
    },
    getInfo(id){
      this.$emit('get-info', id)
    }
  }
}
</script>

<style scoped>
  .grid{
    display:grid;
    grid-template-columns: 5.9fr 5.8fr 20.4fr 14.4fr 15.8fr 6.8fr 8.8fr 8.8fr 13.7fr;
    font-weight: 400;
    font-size: 12px;
    line-height: 120%;
  }

  .grid_header{
    background: #F2F2F2;
    color:#737D8A;
    padding: 12px 0;
  }

  .grid_body{
    color:#3F3F3F;
  }



</style>
