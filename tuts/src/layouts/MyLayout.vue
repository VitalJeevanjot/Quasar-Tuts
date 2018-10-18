<template>
  <q-layout>
    <q-layout-header class="shadow-4">
      <q-toolbar :inverted="$q.theme==='ios'" align="center">
          <q-toolbar-title>
            Steem App
          </q-toolbar-title>
      </q-toolbar>
    </q-layout-header>
    <q-page-container>
      <q-page>
        <q-input v-model="steemUsername" inverted color="secondary"/>
        <div align="center" class="q-pt-md">
        <q-btn label = "Click" @click="checkName">
        </q-btn>
        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MyLayout',
  data () {
    return {
      steemUsername: ''
    }
  },
  methods: {
    checkName: async function () {
      console.log('working!- ')
      if (this.steemUsername === '') {
        this.$q.notify('Please Enter A Value')
        return
      }
      let accounts = await this.$steemClient.database.getAccounts([this.steemUsername])
      console.log(accounts)
      this.$q.notify(accounts[0].balance)
    }
  }
}
</script>

<style>
</style>
