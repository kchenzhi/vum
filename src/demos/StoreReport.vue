<template>
  <div class="page">
    <simple-header title="库存报表" :back-link="true" :onFresh="refresh"></simple-header>
    <page-content>
      <scroll :on-refresh="refresh" :on-infinite="refresh">
        <div class="grid-demo">
          <div class="grids grids-small">
            <template v-for="rows in report">
              <template v-for="p in rows">
                <a href="javascript:;" class="grid">
                  <p class="grid_label" style="word-wrap:break-word;height: 9px">
                    {{p}}
                  </p>
                </a>
              </template>
            </template>
          </div>
        </div>
      </scroll>
    </page-content>
  </div>
</template>
<script>
  import { SimpleHeader } from '../components/header'
  import Content from '../components/content'
  import Scroll from '../components/scroll'

  export default {
    data () {
      return {
        report: []
      }
    },
    components: {
      SimpleHeader,
      'page-content': Content,
      Scroll
    },
    mounted: function () {
      var _self = this
      this.$ajax.get('/order/storeReport').then(function (response) {
        _self.report = response.data
      })
    },
    methods: {
      refresh () {
        var _self = this
        this.$ajax.get('/order/storeReport').then(function (response) {
          _self.report = response.data
        })
      }
    }
  }
</script>
