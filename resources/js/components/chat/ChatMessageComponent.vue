<template>
  <div class="chat-list mb-2 border rounded p-2" >
      <div class="messages" v-for="(chat,index) in chats" :key="index">
          <div class="user d-flex justify-content-between align-items-center">
              <span class="badge badge-primary shadow-sm" v-if="chat.user.name==current_user">{{chat.user.name}}</span>
              <span class="badge badge-secondary shadow-sm" v-else>{{chat.user.name}}</span>
              
              <span class="time badge badge-light shadow-sm">{{chat.created_at}}</span></div>
          <div class="message">
              "{{chat.subject}}"          
              </div>
      <hr class="divider">
      </div>
      
      
  </div>
</template>

<script>
import BusEvent from '../../bus'

export default {
    data(){
        return{
            chats:[],
            current_user:Laravel.user.name
        }
    },
    mounted() {
        this.getAllChats();
        BusEvent.$on('chat.sent',(newChat)=>{
            // console.log(newChat);
            this.chats.push(newChat);
            this.scrollToBottom();
        });

        
    },
    methods: {
        getAllChats(){
            axios.get('/chat/messages').then(response=>{
            // console.log(response.data);
            this.chats = response.data.reverse();
            this.scrollToBottom();
        })
        },
        scrollToBottom(){
            setTimeout(function(){
                let chatList= document.getElementsByClassName('chat-list')[0];
                chatList.scrollTop = chatList.scrollHeight;

            },1)
            // console.log(chatList);
        }
    },
}
</script>

<style>
.chat-list{
  max-height: 350px;
  overflow-y: scroll;
}
</style>