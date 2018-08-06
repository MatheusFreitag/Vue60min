<template>
  <div>
    <md-dialog-alert
      :md-active.sync="pressed"
      :md-title="title"
      :md-content="format" />
  </div>
</template>

<script>
  export default {
    name: 'modal',
    data: () => ({
      pressed: false,
      title: "",
      format: ""
    }),
    methods:{
        changeState: function(comic){
            this.pressed = true,
            this.title = comic.title,
            this.format = comic.format
        }
    }
  }
</script>
