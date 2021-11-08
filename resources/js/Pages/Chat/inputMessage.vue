<template>
  <div class="relative h-10 m-1">
    <div style="border-top: 1px solid #e6e6e6" class="grid grid-cols-6">
      <input
        type="text"
        v-model="message"
        @keyup.enter="sendMessage()"
        placeholder="Message..."
        class="col-span-5 outline-none p-2 rounded-full"
      />
      <button
        @click="sendMessage()"
        class="
          place-self-end
          bg-gray-500
          hover:bg-blue-500
          p-2
          mt-1
          rounded-full
          text-white
        "
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z"
          />
        </svg>
      </button>
    </div>
  </div>
</template>

<script>
import Input from "../../Jetstream/Input.vue";

export default {
  components: { Input },
  props: ["room"],

  data: function () {
    return {
      message: ''
    }
  },

  methods: {
    sendMessage () {
      if (this.message == '') {
        return;
      }

      axios.post('/chat/room/' + this.room.id + '/message', {
        message: this.message
      })
      .then(res => {
        if(res.status == 201) {
          this.message = '';
          this.$emit('messagesent');
        }
      })
      .catch (err => {
        console.log(err);
      })
    }
  }
};
</script>