<template>
  <div class="page">
    <simple-header title="订单信息" :back-link="true"></simple-header>
    <page-content>
      <form-list>
        <div slot="title">房号: {{room}}</div>
        <template v-for="order,index in orders">
          <div class="item-content" style="margin-left: 15px;" v-if="orders.length>1">订单{{index+1}}:</div>
          <template v-for="p in order.items">
            <form-item>
              <div class="item-media">
                <!--<img src="../assets/images/form/i-form-name.png" alt="" width="30"/>-->
              </div>
              <div class="item-content">
                <div class="item-title label">{{p.goods.name}}</div>
                <div class="item-input">
                  <input type="text" v-model="p.meta.total">
                </div>
              </div>
            </form-item>
          </template>
        </template>
      </form-list>
      <div class="content-block content-padded">
        <div class="row">
          <div class="col-50">
            <m-button type="danger" size="large" v-back-link>返回</m-button>
          </div>
          <div class="col-50">
            <m-button size="large" @click.native="finishOrder">收货</m-button>
          </div>
        </div>
      </div>
      <toast text="操作失败!" type="error" ref="t2"></toast>
    </page-content>
  </div>
</template>

<script>
  import { SimpleHeader } from '../components/header'
  import { Button } from '../components/buttons'
  import Content from '../components/content'
  import { Form, FormItem } from '../components/form'
  import Switcher from '../components/switcher'
  import Toast from '../components/toast'
  export default {
    components: {
      SimpleHeader,
      'page-content': Content,
      'm-button': Button,
      Switcher,
      'form-list': Form,
      Toast,
      FormItem
    },
    data () {
      return {
        orders: [],
        room: ''
      }
    },
    asyncComputed: {
      roomOrders () {
        return this.$ajax.get('/order/' + this.room).then(function (response) {
          return response.data
        })
      }
    },
    mounted: function () {
      this.room = this.$route.query.room
      var _self = this
      this.$ajax.get('/order/' + this.room).then(function (response) {
        _self.orders = response.data
      })
    },
    methods: {
      finishOrder () {
        var _self = this
        this.orders.forEach(order => { order.status = 'finished' })
        this.$ajax.put('/order/updateOrder', this.orders).then(function (response) {
          if (response.data.code === 200) {
            _self.$router.push({path: '/result'})
          } else {
            _self.$refs.t2.open()
          }
        })
      }
    }
  }
</script>
