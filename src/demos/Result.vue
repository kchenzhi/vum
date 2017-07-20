<template>
  <div class="page">
    <simple-header title="提示" :back-link="true"></simple-header>
    <page-content>
      <result type="success">
        <div slot="title">操作成功</div>
        <div slot="text">
          <br>
          <br>
        </div>
        <div slot="buttons">
          <m-button @click.native="ok">OK</m-button>
        </div>
      </result>
    </page-content>
  </div>
</template>

<script>
  import { SimpleHeader } from '../components/header'
  import Content from '../components/content'
  import { Button } from '../components/buttons'
  import Result from '../components/result'

  export default {
    components: {
      SimpleHeader,
      'page-content': Content,
      Result,
      'm-button': Button
    },
    methods: {
      ok () {
        this.$router.push({path: '/contacts'})
      }
    }
  }
</script>
