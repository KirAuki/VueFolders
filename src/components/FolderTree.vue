<template>
    <ul class="folder-tree">
        <li v-for="folder in folders" :key="folder.id" class="folder-tree__item" >
            <div @click="toggleFolder(folder.id)" class="folder-tree__folder" >
                <p class="folder-tree__name">{{ folder.name }}</p>
                <span v-if="folder.children.length" class="folder-tree__toggle">[+/-]</span>
            </div>
            <FolderTree 
                v-if="openFolders.includes(folder.id)"
                :folders="folder.children"
                @select="selectFolder"
                class="folder-tree__subtree"
            />
        </li>
    </ul>
</template>


<script lang="ts" setup>
import { ref } from 'vue';

const props = defineProps<{folders:{id: number; name: string; children: any[] }[]}>()
const emit = defineEmits<{(e: 'select', folderId: number): void}>()

const openFolders= ref<number[]>([])
const toggleFolder = (id: number) => {
    if (openFolders.value.includes(id)) {
        openFolders.value = openFolders.value.filter((folderId) => folderId !== id)
    } else {
        openFolders.value.push(id)
    }
}

const selectFolder = (folderId: number) => {
    emit('select', folderId)
}
</script>


<style scoped>
.folder-tree {
    display: flex;
    gap: 10px;
    flex-direction: column;
    list-style: none;
}

.folder-tree__item {
    padding: 5px;
}

.folder-tree__folder {
    cursor: pointer;
    padding: 5px;
}
</style>