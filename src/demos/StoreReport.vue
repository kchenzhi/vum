<template>
  <div class="page">
    <simple-header title="库存报表" :back-link="true"></simple-header>
    <page-content>
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
    </page-content>
  </div>
</template>
<script>
  import { SimpleHeader } from '../components/header'
  import Content from '../components/content'

  export default {
    data () {
      return {
        report: []
      }
    },
    components: {
      SimpleHeader,
      'page-content': Content
    },
    mounted: function () {
      var _self = this
      this.$ajax.get('/order/storeReport').then(function (response) {
        _self.report = response.data
      })
    }
  }
</script>
