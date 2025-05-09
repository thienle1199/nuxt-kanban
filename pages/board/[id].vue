<script setup lang="ts">
    const supabase = await useSupabaseClient();
    const route = useRoute();
    const { data } = useAsyncData('boards', async () => {
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
    .eq("id", Number(route.params.id))
    .single()

    return data
    })
  
</script>

<template>
    <h1>Board page</h1>
    <p>{{ $route.params.id }}</p>
    <pre>
        {{ JSON.stringify(data) }}
    </pre>
</template>