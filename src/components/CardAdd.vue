<template>
  <form :class="classList" @submit.prevent="addCardToList">
    <input v-model="body"
           type="text"
           class="text-input"
           placeholder="Add new card"
           @focusin="startEditing"
           @focusout="finishEditing"
    />
    <hr>
    <input v-model="content" 
           type="text"
           class="text-input"
           placeholder="content"
           @focusin="startEditing"
           @focusout="finishEditing"
      />
          
    <button type="submit"
            class="add-button"
            v-if="isEditing || contentExists">
      Add
    </button>
  </form>
</template>
<script>
  export default {
    props:{
      listIndex: {
        type: Number,
        required: true
      },
    },
    data: function(){
      return {
        body: "",
        content: "",
        isEditing: false,
      }
    },
    computed: {
      classList() {
        const classList = ['addcard']
        if (this.isEditing) {
          classList.push('active')
        }
        if (this.contentExists){
          classList.push('addable')
        }
        return classList
      },
      contentExists() {
        if (this.body != "" || this.content != ""){
          return true
        }else{
          return false
        }
      }
    },
    methods: {
      addCardToList: function(){
        this.$store.dispatch('addCardToList', {body: this.body, content: this.content, listIndex: this.listIndex})
        this.body = ""
        this.content = ""
      },
      startEditing: function() {
        this.isEditing = true
      },
      finishEditing: function() {
        this.isEditing = false
      },
    }
  }
</script>


