<template>
    <div class="users">
        <h1>Users</h1>
        <ul>
            <input type="text" v-model="newUser.name" placeholder="Enter name"/>
            <br>
            <input type="text" v-model="newUser.email" placeholder="Enter email"/>
            <br>
            <input type="submit" v-on:click="addUser" value="Submit"/>
            <li v-for="user in users">
                <input type="checkbox" class="toggle" v-model="user.contacted"/>
                <span :class="{contacted: user.contacted}">
                    {{user.name}} : {{user.email}} <button v-on:click="deleteUser(user)">X</button>
                </span>
            </li>
            
            <!--https://jsonplaceholder.typicode.com/users
            https://www.youtube.com/watch?v=z6hQqgvGI4Y
            53:45
            -->
            
        </ul>
    </div>
</template>

<script>
    export default{
        name: 'users',
        
        data() {
            return {
                newUser: {},
                users: []
            }
        },
        methods: {
            addUser: function(){
                this.users.push({
                    name: this.newUser.name,
                    email: this.newUser.email,
                    contacted: false
                })
                console.log('add')
            },
            deleteUser: function(user){
                this.users.splice(this.users.indexOf(user), 1)
            }
        },
        created: function(){
            this.$http.get('https://jsonplaceholder.typicode.com/users')
            .then(function(response){
                this.users = response.data
            })
        }
    }
</script>

<style scoped>
    .contacted{
        text-decoration: line-through;
    }
</style>