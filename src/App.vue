

<template>
    <div class="app">
        <button  @click="isWindowOpen = true" class="app__open-button">Открыть</button>
        <FoldersWindow 
          v-if="isWindowOpen"
          :title="'Выбирите папку'"
          :isOpen="isWindowOpen"
          @close="closeWindow"
          @select="handleFolderSelect"
          class="app__modal"
        >
            <FolderTree :folders="mockFolders" @select="setSelectedFolder" />
        </FoldersWindow>
    </div>
</template>

<script setup lang="ts">
    import { ref } from 'vue';
    import FoldersWindow from './components/FoldersWindow.vue'
    import FolderTree from './components/FolderTree.vue'

    const isWindowOpen = ref(false)
    const selectedFolderID = ref<number | null>(null)

    const mockFolders = [
        { id: 1, name: 'Папка 1', children: [
            { id: 2, name: 'Папка 1.1', children: [] },
            { id: 3, name: 'Папка 1.2', children: [
                { id: 4, name: 'Папка 1.2.1', children: [] }
            ]}
        ]},
        { id: 5, name: 'Папка 2', children: [] },
    ];

    const closeWindow = () => {
        isWindowOpen.value = false
    }
    const setSelectedFolder = (folderId: number) => {
        selectedFolderID.value = folderId
    }

    const handleFolderSelect = (folderId: number) => {
        console.log(`Выбрана папка с ID: ${folderId}`)
        setSelectedFolder(folderId)
        closeWindow()
    }

</script>

<style scoped>
.app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-size: 16px;
}

.app__open-button {
  padding: 10px 20px;
  cursor: pointer;
}
</style>
