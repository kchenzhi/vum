<template>
  <div class="page">
    <simple-header title="入库" :back-link="true"></simple-header>
    <page-content>
      <form-list>
        <template v-for="p in stores">
          <form-item>
            <div class="item-media">
              <!--<img src="../assets/images/form/i-form-name.png" alt="" width="30"/>-->
            </div>
            <div class="item-content">
              <div class="item-title label">{{p.goodsName}}</div>
              <div class="item-input">
                <input type="text" v-model="p.num">
              </div>
            </div>
          </form-item>
        </template>
        <div slot="append"></div>
      </form-list>
      <div class="content-block content-padded">
        <div class="row">
          <div class="col-50">
            <m-button type="danger" size="large" @click.native="clear">清空</m-button>
          </div>
          <div class="col-50">
            <m-button size="large" @click.native="finishOrder">确定</m-button>
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
        stores: []
      }
    },
    mounted: function () {
      var _self = this
      this.$ajax.get('/goods/name').then(function (response) {
        _self.stores = response.data
      })
    },
    methods: {
      finishOrder () {
        var _self = this
        this.$ajax.post('/store/', this.stores.filter(store => store.num > 0)).then(function (response) {
          if (response.data.code === 200) {
            _self.$router.push({path: '/result'})
          } else {
            _self.$refs.t2.open()
          }
        })
      },
      clear () {
        this.stores.forEach(store => { store.num = 0 })
      }
    }
  }
</script>
