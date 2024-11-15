<template>
  <div
    class="chatInner flex items-start gap-2.5 mb-6"
    v-if="chat.contentType !== 'note'"
  >
    <div class="detail">
      <p
        v-if="chat.contentType === 'bot'"
        class="bg-gray-100 rounded-xl rounded-tl-none py-4 px-6 text-sm mb-2"
      >
        {{ JSON.parse(chat.botLinkedData?.currentBot)?.name }}
      </p>
      <p
        v-if="chat.contentType === 'text'"
        class="bg-gray-100 rounded-xl rounded-tl-none py-4 px-6 text-sm mb-2"
      >
        {{ chat.content }}
      </p>
      <p class="text-gray-500 text-xs flex items-center gap-1">
        {{ chat?.sender?.firstName || chat?.sender?.email.split("@")[0] }}
        <fa :icon="['fas', 'circle']" class="text-[0.5rem] text-gray-500"></fa>
        {{ moment(new Date(chat?.createdAt)).fromNow() }} from
        {{ chat?.sentFrom }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import moment from "moment";

const props = defineProps({
  chat: {
    type: Object,
    default: {},
  },
  sendMessage: {
    type: Function,
    default: () => {},
  },
});
</script>
<style scoped>
.file-div {
  height: 100px;
  width: 100px;
}

.detail {
  margin-top: 20px;
}
</style>
