<script setup lang="ts">
import { cn } from './lib/utils';

const supbase = useSupabaseClient();
const { data } = useAsyncData('boards', async () => {
  const { data } = await supbase.from('boards').select('*')
  return data
})

const isSidebarVisible = true;
</script>
<template>
  <NuxtLayout>
    <aside :class="cn(
      'fixed top-0 left-0 hidden h-full z-40 w-[300px] border-r overflow-hidden border-divider py-6 pr-6 mobile:flex flex-col bg-sidebar',
      {
        'translate-x-0': isSidebarVisible,
        '-translate-x-full': !isSidebarVisible,
        'transition-transform duration-300 ease-in-out': true,
      }
    )">
      <h2 className="text-xs font-bold tracking-[.2em] px-6 mb-4">
        ALL BOARDS ({{ data?.length }})
      </h2>
      <div v-for="board in data" :key="board.id">
        <BoardItem :name="board.name" :id="board.id" />
      </div>
    </aside>
    <div data-sidebar-container className="flex flex-1 flex-col overflow-auto transition-[padding] duration-300 tablet:pl-[300px] data-[sidebar-hidden=true]:pl-0">
      <main className="flex-1 overflow-auto flex flex-col">
        <NuxtPage />
      </main>
    </div>

  </NuxtLayout>
</template>
