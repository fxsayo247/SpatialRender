<template>
    <div class="prompt-container">
        <label class="label-text" for="prompt">Prompt</label>
        <textarea
            v-model="message"
            placeholder="ask me a question"
            class="prompt-input"
            id="prompt"
        >
        </textarea>
        <button
            @click="handlePromptSubmit"
            class="submit-button"
            type="submit"
            :disabled="!message.trim()"
            title="Submit"
            aria-label="Submit prompt"
        >
            <CIcon :icon="cilArrowRight" size="lg"/>
        </button>
    </div>
</template>
<script>
import { CIcon } from '@coreui/icons-vue';
import { cilArrowRight } from '@coreui/icons';

    export default {
        name: 'PromptInput',
        components: {
            CIcon,
        },
        data() {
            return {
                message: '',
                cilArrowRight,
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
    padding: 8px 8px 8px 24px;
    border: 1px solid #ccc;
    border-radius: 50px;
    max-width: 1400px;
    margin: 1rem auto;
    width: 100%;
}
.prompt-input {
    box-sizing: border-box;
    flex-grow: 1;
    border: none;
    outline: none;
    font-size: 1rem;
    background: transparent;
    padding: 15px 10px;
    resize: none;
    height: 50px;
    text-align: left;
}


.submit-button {
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: background-color 0.2s;
    flex-shrink: 0; /* Prevent button from shrinking */
}
.label-text {
    border-right: 1px solid black;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 5px;
}
.submit-button:hover:not(:disabled) {
    background-color: #0056b3;
}
.submit-button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}
</style>