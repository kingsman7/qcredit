<template>
  <div>
    <div class="box box-auto-height q-mb-md">
      <page-actions icon="fas fa-wallet" :title="$tr('qcredit.layout.label.wallet')" @refresh="init" :extra-actions="extraPageActions"/>
    </div>
    <div class="box box-auto-height q-mb-md">
      {{ this.$tr('qcredit.layout.label.amountAvailable') + ": " + this.amountAvailable
      }}
    </div>
    <crud :crud-data="import('@imagina/qcredit/_crud/wallet')"
          @created="$store.dispatch('quserAuth/AUTH_UPDATE')"
          @updated="$store.dispatch('quserAuth/AUTH_UPDATE')"/>
  </div>
</template>

<script>
export default {
  name: "wallet",
  data(){
    return{
      amountAvailable: null,
      actions: true,
    }
  },
  mounted(){
    this.$nextTick(function () {
      this.init()
    })
  },
  computed:{
    //Extra Page actions
    extraPageActions() {
      return [
        {//action to copy user resource link, new reservation
          vIf: this.actions ? true : false,
          props: {
            label: this.$tr(`qcredit.layout.label.withdrawal`),
            rounded: true,
            round: false,
            color: 'green',
            padding: '3px 15px'
          },
          action: () => {

          }
        },
      ]
    },
  },
  methods:{
    //init
    async init() {
      this.loadPage()
      this.$root.$on('page.data.refresh', () => {
        this.loadPage()
      })
    },
    async loadPage() {
      this.loading = true
      await Promise.all([
        this.getAmountAvailable()
      ])
      this.loading = false
    },
    async getAmountAvailable(){
      let requestParams = {
        refresh: true,
        params: { filter: {customerId: this.$store.state.quserAuth.userId, amountAvailable: true } }
      }
      this.$crud.index('/icredit/v1/credits', requestParams).then(async (res) =>{
        this.amountAvailable = await res.data[0].amount
      }).catch(err => console.log(err))
    },
  }
}
</script>

<style scoped>

</style>