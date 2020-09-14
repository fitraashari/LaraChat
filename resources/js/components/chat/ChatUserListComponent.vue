<template>
                    
                    <div class="card">
                    <div class="card-header bg-success text-light">
                        Users online ({{users.length}})
                        </div>
                    <div class="card-body">
                        <ul class="list-group">
                            <li class="list-group-item" v-for="user in users" :key="user.id">
                                <span class="badge badge-success badge-pill">Online</span>
                                {{user.name}}
                                </li>
                        </ul>
                    </div>
                </div>
</template>

<script>
import BusEvent from '../../bus'
    export default {
        data(){
            return{
                users:[]
            }
        },
        mounted() {
            // console.log('Component mounted.')
            BusEvent.$on('chat.here',(users)=>{
                this.users = users
            }).$on('chat.joining',(user)=>{
                this.users.push(user);
            }).$on('chat.leaving',(user)=>{
                this.users = this.users.filter((u)=>{
                    return u.id !== user.id;
                });
            });
        }
    }
</script>
