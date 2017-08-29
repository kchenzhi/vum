<template>
  <div class="page">
    <simple-header title="取货时间汇总" :back-link="true" :onFresh="refresh"></simple-header>
    <page-content>
      <div class="grid-demo">
        <div class="grids grids-small">
          <template v-for="rows,index in report">
            <template v-for="(p,index) in rows">
              <a href="javascript:;" class="grid" style="height: 100px" :id="rows[0]">
                <p class="grid_label" :id="rows[0]">
                  {{p}}
                </p>
              </a>
            </template>
          </template>
        </div>
      </div>
    </page-content>
  </div>
</template>
<script>
  import {SimpleHeader} from '../components/header'
  import Content from '../components/content'

  export default {
    data () {
      return {
        report: [
          ['房号', '周六晚上八点取货八点取货', '房号', '取货时间', '取货时间'],
          ['9A408', '周六晚上']
        ]
      }
    },
    components: {
      SimpleHeader,
      'page-content': Content
    },
    mounted: function () {
      var _self = this
      this.$ajax.get('/order/takeTimeSumReport').then(function (response) {
        _self.report = response.data
      })
    },
    methods: {
      refresh () {
        var _self = this
        this.$ajax.get('/order/takeTimeSumReport').then(function (response) {
          _self.report = response.data
        })
      },
      toList (e) {
        this.$router.push({path: '/form', query: {room: e.currentTarget.id}})
      },
      toOrder (e) {
        this.$router.push({path: '/form', query: {room: e.currentTarget.id}})
      }
    }
  }
</script>
