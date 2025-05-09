<script setup lang="ts">

</script>
<template>
  <NuxtLayout>
    <Sidebar />
    <div data-sidebar-container className="flex flex-1 flex-col overflow-auto transition-[padding] duration-300 tablet:pl-[300px] data-[sidebar-hidden=true]:pl-0">
      <main className="flex-1 overflow-auto flex flex-col">
        <NuxtPage />
      </main>
    </div>

  </NuxtLayout>
</template>
