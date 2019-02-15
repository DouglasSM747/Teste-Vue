<template>
     <v-container fluid grid-list-xl>

      <v-layout column>
        <v-flex>
            <v-layout>
                <v-flex d-flex xs12 sm12 md12>
              
                  <v-data-table :headers="mainHeaders"
                                :items="mainItems"
                                item-key="name"
                                hide-actions
                                class="elevation-1">

                    <template slot="items" scope="props">
                      <tr>
                        <td>  
                          <v-list-tile-avatar> 
                            <img :src="props.item.owner.avatar_url"> 
                          </v-list-tile-avatar>
                        </td>
                        <td class="text-xs">{{props.item.name}}</td>
                        <td class="text-xs">{{ props.item.private }}</td>
                        <td class="text-xs">{{ props.item.size }}</td>
                      </tr>
                    </template>
               
                  </v-data-table>
                </v-flex>
            </v-layout>
        </v-flex>
      </v-layout>
   </v-container>

</template>

<script>

import axios from 'axios'
export default {

  name:"menu",
  data () {
    return {
      mainHeaders: [
          { text: '', value: 'avatar' },
          { text: 'Name Repository', value: 'name' },
          { text: 'Privado', value: 'star' },
          { text: 'Size', value: 'forks' }
      ],
      mainItems: [
      ]
    }
  },
  methods: {
  },
  mounted(){
    var self = this;
    axios.get('https://api.github.com/user/repos?access_token=2852ee5b0e3e6a56c17b59ea8609f1b917b9a934')
    .then(function(res){
      self.mainItems = res.data;
      //console.log(self.mainItems[0].name);
    })
    .catch(function(error){
      console.log('Erro: ',error);
    })
  }
}
</script>
