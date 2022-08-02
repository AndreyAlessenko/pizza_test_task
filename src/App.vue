<template>

  <div class="head"/>
  <div class="wrapper">
    <Header :title="'Список пицц'"/>

    <div class="panel">
      <span>Найдено <strong>{{ amount }}</strong> супер-пицц</span>
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

  <div v-if="showInfo">
    <the-modal-info
        :id="infoID"
        :item="infoItem"
        @close="showInfo = !showInfo"
    />
  </div>

  <div v-if="showCreate">
    <the-modal-create
        @close="showCreate = !showCreate"
    />
  </div>



</template>

<script>
import Header from './components/AppHeader'
import AppButton from './components/AppButton'
import AppTable from './components/TheTable'
import TheModalDel from '@/components/Modal/TheModalDel'
import TheModalInfo from '@/components/Modal/TheModalInfo'
import TheModalCreate from '@/components/Modal/TheModalCreate'


export default {
  mounted() {
    console.log('mounted')
    fetch('https://test6.yucrm.ru/graphapi', {
      method: 'POST',
      headers: {
        BEARER: this.apiKey,
        Accept:'application/json',
        "Content-type":'application/json',
        Connection:'keep-alive',
      },
      body: JSON.stringify({
        query: "{pizza_list{items(limit:10,offset:0){author_phone comment size thickness spicy weight id name create_time change_time}count}}"
      })
    }).then(res => res.body).then(response => {
          const reader = response.getReader()
              return new ReadableStream({
                start(controller) {
                  function push() {
                    reader.read().then(({done, value}) => {
                      if (done) {
                        controller.close();
                        return;
                      }
                      controller.enqueue(value);
                      push();
                    });
                  }
                  push();
                },
              })

        })
        .then((stream) =>
            new Response(stream, { headers: { 'Content-Type': 'text/html' } }).text()
        )
        .then((result) => {


          const data = JSON.parse(result).data
          this.amount = data.pizza_list.count
          console.log(data)
          this.pizzaList =  data.pizza_list.items.map(item =>{

            item.size = this.getItemSize(item.size) + ' см'
            const thickness = this.getItemThickness(item.thickness)
            item.thickness = thickness.name
            item.price = item.weight * thickness.mult + ' ₽'
            item.create_time = new Date(item.create_time).toLocaleDateString()

            return item
          })
        });


  },
  data() {
    return {
      amount: 0,
      apiKey: '8ad8757baa8564dc136c1e07507f4a98',
      showDel:false,
      deletedID:'',
      deletedName:'',
      showInfo:false,
      infoID:'',
      infoItem:'',
      showCreate:false,
      pizzaList:[]
    }
  },
  methods: {
    addPizza() {
      this.showCreate = true
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
      this.showInfo = true
      this.infoID = id
      this.infoItem = this.pizzaList.find(item => item.id === id)
      console.log(`Getting info about pizza id: ${id}...`)
    },
    getItemSize(size){
      switch(size){
        case 'SIZE_23': return '23'
        case 'SIZE_25': return '25'
        case 'SIZE_30': return '30'
        default: return 0
      }
    },
    getItemThickness(thickness){
      switch(thickness){
        case 'THICK': return {name:'Тонкое', mult: 1}
        case 'THIN': return {name:'Традиционное', mult: 2}
        case 'ULTRA_THIN': return {name:'Ультратонкое', mult: 3}
        default: return {name:'', mult: 0}
      }
    }
  },
  components: {
    Header, AppButton, AppTable, TheModalDel, TheModalInfo, TheModalCreate,
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
