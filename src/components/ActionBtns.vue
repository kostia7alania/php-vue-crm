<template>
  <v-card-actions class="white justify-center">

    <v-tooltip 
        v-for="(action, i) in actions" 
        :key="i"
        bottom
    >
      <template v-slot:activator="{ on }">
      
        <v-btn
          :disabled="!IS_ADMIN"
          v-on="on"
          dark 
          :color="action.color"
          class="white--text ml-1" 
          fab
          icon
          small
          @click.stop="actionClick(action.method)"
        >
        <v-icon>{{ action.icon }}</v-icon>
       </v-btn>
      </template>
      <span>{{action.tooltip}}</span>
    </v-tooltip>
   
  </v-card-actions>
</template>
<script> 
import { mapState } from 'vuex'
  export default { 
    props: ['item'],
    data() {
      return {
        actions: [ 
            {
              method: 'edit',
              icon: 'edit',
              tooltip: 'Click to edit',
              color: 'cyan darken-1'
            },
            {
              method: 'delete',
              icon: 'delete_outline',
              tooltip: 'Click to delete',
              color: 'red  '
            }
          ]

      }
    },
    computed: {
      ...mapState([
        'IS_ADMIN'
      ])
    },
    methods: {
      actionClick(e) {
        if(e == 'edit' ) this.$emit('edit', this.item)
        else if(e == 'delete') this.$emit('delete', this.item)
        // else this.$emit(e) // just for example
      }
    }
  }
</script>
 