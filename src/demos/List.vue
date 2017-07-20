<template>
  <div class="page">
    <simple-header title="订单信息" :back-link="true"></simple-header>
    <page-content>
      <list>
        <div slot="title">{{room}}</div>
        <template v-for="order in roomOrders">
          <template v-for="p in order.items">
            <list-item>
              <div class="item-content">
                <div class="item-title-row">
                  <div class="item-title" style="margin-left: 50px">{{p.goods.name}}</div>
                  <div class="item-after" style="margin-right: 50px"><input type="text"></div>
                </div>
              </div>
            </list-item>
          </template>
        </template>
      </list>
      <div class='content-padded'>
        <div class="content-block">
          <div class="row">
            <div class="col-50">
              <m-button size="middle" type="danger">返回</m-button>
            </div>
            <div class="col-50">
              <m-button size="middle">收货</m-button>
            </div>
          </div>
        </div>
      </div>
    </page-content>
  </div>
</template>

<script>
  import { SimpleHeader } from '../components/header'
  import { Button } from '../components/buttons'
  import Content from '../components/content'
  import { List, ListItem } from '../components/list'
  import Switcher from '../components/switcher'

  export default {
    data () {
      return {
        orders: [
          {
            room: '9A408',
            items: [{goodsName: '黑美人', num: 9}, {goodsName: '夏黑', num: 2}]
          }
        ],
        room: ''
      }
    },
    components: {
      SimpleHeader,
      'page-content': Content,
      List,
      ListItem,
      Switcher,
      'm-button': Button
    },
    asyncComputed: {
      roomOrders () {
        return this.$ajax.get('/order/' + this.room).then(function (response) {
          console.log(response.data)
          return response.data
        })
      }
    },
    mounted: function () {
      this.room = this.$route.query.room
      this.orders = this.$ajax.get('/order/' + this.room).then(function (response) {
        return response.data
      })
    }
  }
</script>
