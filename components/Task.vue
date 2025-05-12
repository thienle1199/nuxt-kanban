<script setup lang="ts">
      const props = defineProps({
        title: { type: String, required: true },
    // isActive: { type: Boolean, default: false }
  })

</script>
<template>
    <div
        class="p-4 min-w-[280px] bg-white dark:bg-dark-grey rounded-lg mb-2 cursor-pointer hover:opacity-80 transition-opacity">
        <h3 class="text-foreground-contrast font-bold mb-2">{{props.title}}</h3>
        <!-- <p class='text-foreground text-xs'>
            {subTaskCompleted} of {sub_tasks?.length} Subtasks
        </p> -->
        <p class='text-foreground text-xs'>
            0 of 1 Subtasks
        </p>
    </div>
</template>