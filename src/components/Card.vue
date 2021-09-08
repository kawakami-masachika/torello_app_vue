<template>
  <div class="card">
    <button class="close-button" @click="removeCardFromList">✕</button>
    <div class="body">
      <p>タイトル：{{body}}</p>
      <p>内容：{{content}}</p>
    </div>
  </div>
</template>
<script>
  export default{
    props:{
      body:{
        type: String,
        required: true
      },
      content:{
        type: String,
        required: true
      },
      listIndex:{
        type: Number,
        required: true
      },
      cardIndex:{
        type: Number,
        required: true
      }
    },
    methods:{
      removeCardFromList: function(){
        if(confirm('本当にこのカードを削除しますか？')){
          this.$store.dispatch('removeCardFromList', {cardIndex: this.cardIndex, listIndex: this.listIndex})
        }
      }
    },
  }
</script>
