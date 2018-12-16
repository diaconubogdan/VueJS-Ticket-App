<template>
  <div>
    <p>Completed Tasks: {{tickets.filter(ticket => {return ticket.done === true}).length}}</p>
    <p>Pending Tasks: {{tickets.filter(ticket => {return ticket.done === false}).length}}</p>
    <ticket  v-on:delete-ticket="deleteTicket" v-on:complete-ticket="completeTicket" v-for="ticket in tickets" v-bind:ticket="ticket" :key="ticket.id"></ticket>
  </div>
</template>

<script type = "text/javascript" >
import sweetalert from 'sweetalert'
import Ticket from './Ticket'

export default {
  props: [ 'tickets' ],
  components: {
    Ticket
  },
  methods: {
    deleteTicket (ticket) {
      sweetalert({
        title: 'Are you sure?',
        text: 'This ticket will be permanently deleted!',
        icon: 'warning',
        buttons: true
      })
        .then((isConfirm) => {
          if (isConfirm) {
            const ticketIndex = this.tickets.indexOf(ticket)
            this.tickets.splice(ticketIndex, 1)
            sweetalert('Deleted!', 'Your ticket has been deleted.', 'success')
          }
        })
    },
    completeTicket (ticket) {
      const ticketIndex = this.tickets.indexOf(ticket)
      this.tickets[ticketIndex].done = true
    }
  }
}
</script>
<style>
</style>
