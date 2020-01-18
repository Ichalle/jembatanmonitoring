<template>
    <v-layout row wrap>
        <template v-for="(item, index) in items">
            <v-flex :key="index" lg3 sm12 xs12>
                <v-card outlined>
                    <v-card-text class="pa-0">
                    <v-list 
                        two-line 
                        :class="item.priority !== 'low' ? setPriorityColor(item.priority) : ''" 
                        class="lighten-5 pa-0"
                        slot="activator"
                        >
                        <v-list-tile  href="#">
                            <v-list-tile-content>
                                <v-list-tile-title>{{item.title}}</v-list-tile-title>
                                <v-list-tile-sub-title>{{item.longspan}}</v-list-tile-sub-title>
                                <v-list-tile-sub-title>{{item.bentang}}</v-list-tile-sub-title>
                            </v-list-tile-content>
                        </v-list-tile>
                    </v-list>
                    </v-card-text>
                    
                    
                    <v-card-actions :class="setPriorityColor(item.priority)">
                    </v-card-actions>
                    
                </v-card>
            </v-flex>
        </template>
    </v-layout>
</template>
<script>
import notes from '@/api/dashboard-list';
export default {
  data: () => ({
    items: notes
  }),
  computed: {
    setPriorityColor(priority){
        return priority => {
            switch (priority) {
                case 'medium':
                return 'yellow'
                case 'high':
                return 'red'
                default:
                return 'light-green'
            }
        }
    }
  },

  methods: {
    handleClick: (e) => {
      console.log(e);
    }
  },

};
</script>