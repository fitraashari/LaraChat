<template>
  <div>
      <form>
          <div class="form-group">
              <textarea rows="3" class="form-control" placeholder="Isi Pesan Anda Di Sini" v-model="body" @keydown="handleInput"></textarea>
              <!-- <button class="btn btn-primary mt-1 float-right" >Send</button> -->
          </div>
      </form>
  </div>
</template>

<script>
import moment from 'moment';
import BusEvent from '../../bus'
export default {
data(){
    return{
        body:'',
    }
},
methods: {
    handleInput(e){
        if (e.keyCode==13 && !e.shiftKey) {
            e.preventDefault();
            this.sendChat();
        }
    },
    sendChat(){
        let input = this.body.trim();
        if (input === '') {
            return
        }
        let newChat = {
            subject : input,
            created_at: moment().utc(0).format('YYYY-MM-DD HH:mm:ss'),
            user: {
                name:Laravel.user.name
            }
        }
            axios.post('/chat/new',{subject:input}).then(response=>{
                console.log(response);
            })
            BusEvent.$emit('chat.sent',newChat);
             this.body='';
            
    }
},
}
</script>
