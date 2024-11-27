<template>
    <div v-if="isOpen" class="folders-window">
        <div class="folders-window__overlay">            
            <div class="folders-window__content">
                <h2 class="folders-window__title">{{ title }}</h2>
                <slot></slot>
                
                <div class="folders-window__actions">
                    <button @click="closeWindow" class="folders-window__button folders-window__button--close">Закрыть</button>
                    <button @click="confirm" class="folders-window__button folders-window__button--confirm">Ок</button>
                </div>
            </div>
        </div>
    </div>
</template>




<script lang="ts" setup>

const props = defineProps<{ title:string; isOpen: boolean}>()

const emits = defineEmits<{ (e: 'close'): void; (e:'select', folderId: number): void }>()

const closeWindow = () => emits('close')

let selectedFolderID = 0
const confirm = () => emits('select', selectedFolderID)
</script>




<style scoped>

.folders-window {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.folders-window__overlay {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
}

.folders-window__content {
    display: flex;
    align-items: center;
    box-sizing: border-box;
    gap: 20px;
    min-width: 400px;
    justify-content: center;
    flex-direction: column;
    background-color: white;
    padding: 20px;
    color: black;
}

.folders-window__title {
    display: inline;
}

.folders-window__actions {
    display: flex;
    gap: 50px;
}

.folders-window__button {
   max-width: 80px;
   padding: 10px;
   border-radius: 5px;
   border: none;
   color: white;
}
.folders-window__button--close {
    background-color: red;
}
.folders-window__button--confirm {
    background-color: green;   
}
</style>