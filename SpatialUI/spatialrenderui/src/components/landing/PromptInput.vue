<template>
    <div class="prompt-container">
        <label class="label-text" for="prompt'">Insert Question Here:</label>
        <input
            v-model="message"
            placeholder="ask me a question"
            class="prompt-input"
            id="prompt"
        />
        <span>
        <button
            @click="handlePromptSubmit"
            class="submit-button"
            type="submit"
        >
            Prompt
        </button>
        </span>
    </div>
</template>
<script>
// import CIcon from '@coreui/icons-vue';

    export default {
        name: 'PromptInput',
        components: {
            // CIcon
        },
        data() {
            return {
                message: ''
            }
        },
        // props: {
        //     message: {
        //         type: String,
        //         required: true
        //     }
        // }, 
        methods: {
            handlePromptSubmit() {
                this.$emit('prompt-submitted', this.message);
            },

            sendToEndPoint() {

            }
        }
    }
</script>
<style scoped>
.prompt-container {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    max-width: 1400px;
    margin: 1rem auto;
    width: 100%;
    height: 100px;
}
.prompt-input {
    flex-grow: 1;
    border: none;
    outline: none;
    font-size: 1rem;
}
.submit-button {
    background: none;
    border: none;
    cursor: pointer;
    padding: 0.5rem;
}
</style>