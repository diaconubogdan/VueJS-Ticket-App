<template>
  <div class='ui centered card'>
    <div class="content" v-show="!isEditing">
      <div class='header'>
        {{ ticket.title }}
      </div>
      <div class='meta'>
        {{ ticket.description }}
      </div>
      <div class='meta'>
        Risk: {{ ticket.risk }}
      </div>
      <div class='extra content'>
        <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' v-on:click="deleteTicket(ticket)">
          <i class='trash icon'></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="ticket.title" >
        </div>
        <div class='field'>
          <label>Description</label>
          <input type='text' v-model="ticket.description" >
        </div>
        <div class='field'>
          <label>Risk</label>
          <input type='text' v-model="ticket.risk" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Save X
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' v-show="!isEditing &&ticket.done" disabled>
      Completed
    </div>
    <div class='ui bottom attached red basic button' v-on:click="completeTicket(ticket)" v-show="!isEditing && !ticket.done">
      Pending
    </div>
   </div>
</template>

<script>
export default {
  props: ['ticket'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    completeTicket (ticket) {
      this.$emit('complete-ticket', ticket)
    },
    showForm () {
      this.isEditing = true
    },
    hideForm () {
      this.isEditing = false
    },
    deleteTicket (ticket) {
      this.$emit('delete-ticket', ticket)
    }
  }
}
</script>
