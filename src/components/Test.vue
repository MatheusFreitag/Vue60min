<template>
    <div class="test">
        <input type="text" v-model="title"/><br>
        <h1>{{title}}</h1>
        <p v-if="showName">{{user.firstName}}</p>
        <p v-else>Nobody</p>
        <ul>
            <li v-for="item in items">{{item.title}}</li>
        </ul>
        <button v-on:click="greet()">Say Greeting</button>
        <br>
        <input type="text" v-on:keyup="pressKey" v-on:keyup.enter="enterHit"/>
    </div>
</template>

<script>
    export default{
        name: 'test',
        data() {
            return {
                title: 'Hello World',
                user: {
                    firstName: 'Matheus',
                    lastName: 'Freitag'
                },
                showName: true,
                items: [
                    {title: 'Item One'},
                    {title: 'Item Two'},
                    {title: 'Item Three'}
                ]
            }
        },
        methods: {
            greet: function(){
                console.log("Hello from greet!");
            },
            pressKey: function(e){
                console.log(e.target.value)
            },
            enterHit: function(){
                console.log("You hit enter");
            }
        }
    }
</script>

<style scoped>
    
</style>