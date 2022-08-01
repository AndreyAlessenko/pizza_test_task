<template>

  <div class="head"/>
  <div class="wrapper">
    <Header :title="'Список пицц'"/>

    <div class="panel">
      <span>Найдено <strong>{{ pizzaList.length }}</strong> супер-пицц</span>
      <app-button
          :className="'primary'"
          @app-btn-click="addPizza">Добавить пиццу
      </app-button>

    </div>
    <AppTable
        :list="pizzaList"
        @edit-pizza="editPizza"
        @delete-pizza="deletePizza"
        @get-info="getInfo"
    />

  </div>

  <div v-if="showDel">
    <the-modal-del
      :id="deletedID"
      :name="deletedName"
      @close="showDel = !showDel"
      @confirm-deleting="confirmDeleting"
      />
  </div>



</template>

<script>
import Header from './components/AppHeader'
import AppButton from './components/AppButton'
import AppTable from './components/TheTable'
import TheModalDel from '@/components/Modal/TheModalDel'
// import axios from 'axios'


export default {
  async mounted() {
    console.log('mounted')

    const data = await fetch('https://test6.yucrm.ru/graphapi', {
      method: 'POST',
      headers: {
        BEARER: this.apiKey,
        Accept:'application/json',
        "Content-type":'application/json',
        Connection:'keep-alive',
        "Access-Control-Allow-Origin": "http://localhost:8080/"
      },
      mode:'no-cors',
      body: JSON.stringify({
        query: "{pizza_list{items(limit:1,offset:0){author_phone comment size thickness spicy weight id name create_time change_time}count}}"
      })
    })


    console.log(data)
  },
  data() {
    return {
      amount: 5,
      apiKey: '8ad8757baa8564dc136c1e07507f4a98',
      showDel:false,
      deletedID:'',
      deletedName:'',
      infoID:'',
      infoItem:'',
      pizzaList: [
        {
          id: 1,
          name: 'Пицца 1',
          cucumber: 'Малосоленые',
          dough: 'Тонкое',
          size: '23 см',
          spicy: true,
          price: '450 ₽',
          date: '12 мая 2021'
        },
        {
          id: 2,
          name: 'Пицца 2',
          cucumber: 'Соленые',
          dough: 'Традиционное',
          size: '30 см',
          spicy: false,
          price: '450 ₽',
          date: '12 сентября 2021'
        }
      ]
    }
  },
  methods: {
    addPizza() {
      console.log('Adding pizza...')
    },
    editPizza(id) {
      console.log('Adding pizza with id: ', id)
    },
    deletePizza(id) {
      this.showDel = true
      this.deletedID = id
      this.deletedName = this.pizzaList.find(item => item.id === id).name
      console.log(`Deleting pizza with id: ${id}...`)
    },
    confirmDeleting(id){
      let index = this.pizzaList.findIndex(item => item.id === id);
      this.pizzaList.splice(index, 1)
      this.showDel = false
    },
    getInfo(id) {
      this.infoID = id
      this.infoItem = this.pizzaList.find(item => item.id === id)
      console.log(`Getting info about pizza id: ${id}...`)
    }
  },
  components: {
    Header, AppButton, AppTable,TheModalDel
  }
}
</script>

<style>

.panel {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
}

.panel span {
  font-weight: 400;
  font-size: 14px;
  line-height: 120%;
}


</style>
