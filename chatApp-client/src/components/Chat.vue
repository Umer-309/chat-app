<template>
  <main class="px-4 pb-6 relative bg-white rounded-b-[32px]">
    <div
      class="conversationView pt-6"
      v-for="(chat, index) in chatRoomMessages"
      :key="index"
    >
      <p
        class="chatTime text-xs text-center w-full text-gray-500 mb-6 font-light"
      >
        {{ chat._id === moment().format("YYYY-MM-DD") ? "Today" : chat._id }}
        {{ console.log('chat',chat) }}
        {{ "11 Nov 2024" }}
      </p>
      <div v-for="(chat, index) in chat.docs" :key="index">
				{{ console.log('Docs',chat) }}
          <ChatReply
            v-if="chat?.sender?._id === userId"
            :chat="chat"
            :chatRoomAgents="chatRoomAgents"
          />

					<ChatStart v-else :chat="chat" :sendMessage="sendMessage" />
      </div>
    </div>
  </main>
  <Input />
</template>

<script setup>
import { chats } from "@/utils/chats";
import Input from "./Input.vue";
import { ref } from "vue";
import moment from "moment";
import ChatReply from "./ChatReply.vue";
import ChatStart from "./ChatStart.vue";

const userId = ref("673483e301e9610b92abeebf");
const chatRoomMessages = ref([chats]);

const sendMessage = () => {
	console.log('send message')
}
</script>

<style scoped>
:deep(.sendButton svg) {
  font-size: 20px;
}

.file_button svg {
  color: var(--gray-text, #a3a3a3);
  font-family: "Font Awesome 6 Pro";
  font-size: 20px;
  font-style: normal;
  font-weight: 300;
  line-height: normal;
  margin-right: 12px;
}
</style>
