<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable :list="lists" class="list-index" @end="movingList">
        <list v-for="(item, index) in lists"
              :key="item.id"
              :title="item.title"
              :listIndex="index"
              :cards="item.cards"
              @change="movingCard"
        />
        <list-add />
      </draggable>
    </main>
  </div>
</template>

<script>
  import draggable from 'vuedraggable'
  import ListAdd from './ListAdd'
  import List from './List'
  import {mapState} from 'vuex'

  export default{
    name: 'Board',
    components: {
      draggable,
      ListAdd,
      List
    },
    computed: {
      totalCardCount(){
        return this.$store.getters.totalCardCount
      },
      ...mapState([
        'lists'
      ])
    },
    methods: {
      movingCard: function(){
        this.$store.dispatch('updateList', {lists: this.lists})
      },
      movingList: function(){
        this.$store.dispatch('updateList', {lists: this.lists})
      }
    }
  }

</script>