<template>
  <div class="chat-list mb-1" >
      <div class="messages" v-for="(chat,index) in chats" :key="index">
          <div class="user "><span class="badge badge-primary">{{chat.user.name}}</span><span class="time badge badge-light">{{chat.created_at}}</span></div>
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
            chats:[]
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