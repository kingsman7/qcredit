<template>
</template>
<script>
export default {
  data() {
    return {
      crudId: this.$uid(),

    }
  },
  mounted(){

  },
  computed: {

    crudData() {
      return {
        crudId: this.crudId,
        apiRoute: 'apiRoutes.qcredit.credits',
        read: {
          icon: 'fas fa-map-marker-alt',
          search: false,
          columns: [
            {
              name: 'id', label: this.$tr('ui.form.id'), field: 'id',
              align: 'left'
            },
            {
              name: 'amount', label: this.$tr('ui.label.amount'), field: 'amount',
              align: 'left'
            },
            {
              name: 'status', label: this.$tr('ui.form.status'), field: 'status',
              format: val => val || '-', align: 'left'
            },
            {
              name: 'date', label: this.$tr('ui.form.date'), field: 'date',
              align: 'left'
            },
            {
              name: 'description', label: this.$tr('ui.form.description'), field: 'description',
              classes: 'ellipsis', style: 'max-width : 250px', format: val => val || '-', align: 'left'
            },

            //{name: 'actions', label: this.$tr('ui.form.actions'), align: 'left'},
          ],
          requestParams: {filter: {  customerId: this.$store.state.quserAuth.userId}}
        },

      }
    }

  },
  methods: {

  }
}
</script>
