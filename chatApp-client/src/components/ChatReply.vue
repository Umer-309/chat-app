<template>
    <div class="chatInner flex items-start gap-2.5 mb-6 justify-end">
        <div class="detail">
            <p
                v-if="chat.contentType === 'text' || chat.contentType === 'bot'"
                class="bg-purple-400 rounded-xl rounded-tr-none py-4 px-6 text-sm mb-2 text-white"
            >
                {{ chat.content }}
            </p>
            <div v-if="chat.contentType === 'image'">
                <img
                    v-for="(image, index) in chat.content"
                    :key="index"
                    class="bg-gray-100 rounded-xl rounded-tl-none text-sm mb-2 h-40 w-auto"
                    :src="image"
                />
            </div>
            <div v-if="chat.contentType === 'document'">
                <a
                    v-for="(doc, index) in chat.content"
                    :key="index"
                    class="bg-gray-100 rounded-xl rounded-tl-none text-sm mb-2 h-40 w-auto text-blue-500 hover:underline"
                    :href="doc"
                    >{{ doc.split('VOZACHAT/')[1] }}<br
                /></a>
            </div>
            <div v-if="chat.contentType === 'video'">
                <video
                    width="320"
                    height="240"
                    controls
                    v-for="(vid, index) in chat.content"
                    :key="index"
                    class="bg-gray-100 rounded-xl rounded-tl-none text-sm mb-2 h-40 w-auto"
                >
                    <source :src="vid" type="video/mp4" />
                </video>
            </div>
            <div v-if="chat.contentType === 'audio'">
                <audio
                    width="320"
                    height="240"
                    controls
                    v-for="(aud, index) in chat.content"
                    :key="index"
                    class="bg-gray-100 rounded-xl rounded-tl-none text-sm mb-2 h-10"
                >
                    <source :src="aud" type="audio/mpeg" />
                </audio>
            </div>
            <p class="text-gray-500 text-xs flex items-center gap-1">
                {{ moment(new Date(chat.createdAt)).fromNow() }} from
                {{ chat?.sentFrom }}

                <fa :icon="['fas', 'circle']" class="text-[0.5rem] text-gray-500"></fa>
                <span v-if="checkIfMessageSeen() === true">
                    <span class="text-sm text-blue-500 mr-1 leading-[14px]">
                        <fa :icon="['fal', 'check-double']" class="text-sm"></fa> </span
                ></span>
            </p>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import moment from 'moment';
const props = defineProps({
    chat: {
        type: Object,
        default: {}
    },
    chatRoomAgents: {
        type: Array,
        default: []
    }
});

const checkIfMessageSeen = () => {
    let anyAgentSeen = false;
    props.chatRoomAgents.map((agent) => {
        if (props?.chat?.readBy.includes(agent?._id)) {
            anyAgentSeen = true;
            return;
        }
    });
    return anyAgentSeen;
};
</script>

<style scoped>
.file-div {
    height: 100px;
    width: 100px;
}
</style>
