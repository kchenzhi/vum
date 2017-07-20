<template>
  <page-header>
    <header-link v-if="backLink" :left="true" :edge="true" v-back-link>
      <icon icon="back"></icon>
      {{backText}}
    </header-link>
    <page-title @click.native="toIndex">{{title}}</page-title>
    <header-link v-if="onFresh" :right="true" :edge="true" @click.native="refresh">
      刷新
    </header-link>
  </page-header>
</template>

<script>
  import Header from './header'
  import Title from './title'
  import Link from './link'
  import Icon from '../icons'

  export default {
    components: {
      'page-header': Header,
      'page-title': Title,
      'header-link': Link,
      Icon
    },
    props: {
      title: {
        type: String,
        required: true
      },
      backLink: {
        type: Boolean,
        default: false
      },
      backText: {
        type: String,
        default: 'Back'
      },
      onFresh: {
        type: Function
      }
    },
    methods: {
      toIndex () {
        this.$router.push({path: '/'})
      },
      refresh () {
        if (this.onFresh) {
          this.onFresh()
        }
      }
    }
  }
</script>
