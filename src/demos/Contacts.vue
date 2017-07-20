<template>
  <div class="my-page">
    <simple-header title="取货" :back-link="true" :freshText="'取货时间'" :onFresh="toTakeTime"></simple-header>
    <second-header>
      <searchbar @input="onInput"></searchbar>
    </second-header>
    <page-content>
      <div class="grids grids-small">
        <template v-for="p in filtedList">
          <div class="grid" @click="toList" :id="p.recipientAddress" style="width: 70px">
            <!--<router-link :to="{ path: 'list' }" class="grid">-->
            <div class="grid_icon">
              <img src="../assets/images/home/circle.png" alt="">
            </div>
            <p class="grid_label">
              {{p.recipientAddress}}
            </p>
            <!--</router-link>-->
          </div>
        </template>
      </div>
    </page-content>
  </div>
</template>

<script>
  import { SimpleHeader, SecondHeader } from '../components/header'
  import Content from '../components/content'
  import { List, ListItem } from '../components/list'
  import Searchbar from '../components/searchbar'

  export default {
    components: {
      SimpleHeader,
      SecondHeader,
      Searchbar,
      'page-content': Content,
      List,
      ListItem
    },
    data () {
      return {
        input: '',
        list: [],
        room: ''
      }
    },
    asyncComputed: {
      filtedList () {
        return this.$ajax.get('/order/search?room=' + this.room).then(function (response) {
          return response.data
        })
      }
    },
    methods: {
      onInput (v) {
        this.room = v
      },
      toList (e) {
        this.$router.push({path: '/form', query: {room: e.currentTarget.id}})
      },
      toTakeTime (e) {
        this.$router.push({path: '/takeTimeReport'})
      }
    }
  }
</script>
