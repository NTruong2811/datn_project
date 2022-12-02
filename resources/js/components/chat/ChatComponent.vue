<template lang="">
    <div class="w-[300px] h-[400px] bg-white fixed right-[20px] bottom-[50px] rounded-md shadow-lg">
          <div class="head w-full bg-[#FF3F3A] px-4 h-[40px]">
             <span class="text-white">Chăm sóc khach hàng</span>
          </div>
          <div class="content px-4">
              <div class="chat max-h-[300px]">
                       <p>{{user_id}}</p>
              </div>
              <div class="write-text absolute bottom-0">
                 <input type="text" v-model="message">  <button @click="sendMessage">send</button>
              </div>
          </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            message:''
        }
    },
    props: ['user_id'],
    mounted() {
         
    },
    methods: {
        sendMessage(){
            console.log(this.user_id);
            axios.post('/api/send',{
                'message':this.message,
                'sender_id':this.user_id,
                 'box_id':1
            }).then(function(data){
            })

              var channel = window.Echo.channel('channel-chat')
              channel.listen('ChatEvent',function(data){
                  console.log(data);
              })
        }
    },
}
</script>