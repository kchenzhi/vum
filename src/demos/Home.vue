<template>
  <div class="my-page">
    <page-header>
      <header-link>About</header-link>
      <header-title>VUM</header-title>
    </page-header>
    <page-content>

    </page-content>
  </div>
</template>
<script>
import Grid from '../components/grid'
import { Header, HeaderLink, HeaderTitle } from '../components/header'
import Content from '../components/content'

export default {
  components: {
    'page-header': Header,
    HeaderLink,
    HeaderTitle,
    'page-content': Content,
    Grid
  }
}
</script>
