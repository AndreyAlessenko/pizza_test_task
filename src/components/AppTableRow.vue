<template>
  <div class="sell ps-16">{{item.id}}</div>
  <div class="sell item-control">
    <img class="cursor-p" src="../assets/img/edit.svg" alt="" @click="this.$emit('edit-pizza', item.id)">
    <img class="cursor-p" src="../assets/img/delete.svg" alt="" @click="this.$emit('delete-pizza', item.id)">
  </div>
  <div class="sell ps-16 active-sell">
    <span class="item_name cursor-p"  @click="this.$emit('get-info', item.id)">{{ item.name }}</span>
  </div>
  <div class="sell ps-16">{{ item.cucumber }}</div>
  <div class="sell ps-16">{{ item.dough }}</div>
  <div class="sell ta-c">{{ item.size }}</div>
  <div class="sell ta-c">{{ item.spicy ? 'Да':'Нет' }}</div>
  <div class="sell ta-c active-sell">{{ item.price }}</div>
  <div class="sell ta-c">{{ item.date }}</div>
</template>

<script>

export default {
  props:['item'],
  emits:['edit-pizza','delete-pizza', 'get-info']
}
</script>

<style scoped>

.sell{
  border: 1px #F2F2F2 solid;
  padding-top: 16px;
  padding-bottom: 16px;
}

.active-sell{
  color: #00704B;
  font-weight: 600;
}

.item-control{
  display: flex;
  justify-content: space-evenly;
}
.item_name:hover{
  text-decoration:underline
}

</style>
