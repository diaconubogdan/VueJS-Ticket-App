<template>
  <div id="app">
    <h1 class="ui dividing centered header">Vue.js Ticket Manager</h1>
    <div class='ui three column centered grid'>
      <div class='column'>
        <ticket-list v-bind:tickets="tickets"></ticket-list>
        <create-ticket v-on:create-ticket="createTicket"></create-ticket>
      </div>
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert'
import TicketList from './components/TicketList'
import CreateTicket from './components/CreateTicket'

export default {
  name: 'App',
  components: {
    TicketList,
    CreateTicket
  },
  data () {
    return {
      tickets: [{
        id: 1,
        title: 'Login bug',
        description: 'Nothing happens when a user clicks login',
        risk: 2,
        done: false
      }, {
        id: 2,
        title: 'Sign up bug',
        description: 'The submit button is not working',
        risk: 2,
        done: true
      }, {
        id: 3,
        title: 'Post bug',
        description: 'Users cannot post messages',
        risk: 1,
        done: false
      }]
    }
  },
  methods: {
    createTicket (ticket) {
      const id = this.tickets.length + 1
      this.tickets.push({
        id: id,
        title: ticket.title,
        description: ticket.description,
        risk: ticket.risk,
        done: ticket.done
      })
      sweetalert('Success!', 'Ticket added!', 'success')
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
