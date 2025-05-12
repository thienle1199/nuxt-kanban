<script setup lang="ts">
const supabase = await useSupabaseClient();
const { id } = useRoute().params

const { data } = useAsyncData(`board:${id}`, async () => {
  const { data } = await supabase
    .from("boards")
    .select(
      `
      id,
      name,
       columns (
         id,
         name,
         tasks (
            *,
            sub_tasks (
              *
            )
          )
      )
      `
    )
    .eq("id", Number(id))
    .single()

  return data
})

const colorsStatus = [
  "#49C4E5",
  "#8471F2",
  "#67E2AE",
  "#F6C343",
  "#FBAF85",
  "#F24C3D",
]

</script>

<template>
  <div class="flex gap-6 p-6 justify-items-start flex-1">
    <div v-for="(column, index) in data?.columns" class='flex flex-col flex-1 gap-6 min-w-[280px]'>
      <div class="flex items-center gap-3">
        <span class="w-[15px] h-[15px] rounded-full" :style="{ backgroundColor: colorsStatus[index || 0] }"></span>
        <h2 class="text-xs uppercase font-bold">{{ column.name }} ({{ column.tasks?.length }})</h2>
      </div>
      
      <div v-for="task in column.tasks" class="flex flex-col gap-5">
        <Task :title="task.title" />
      </div>
    </div>
  </div>
</template>