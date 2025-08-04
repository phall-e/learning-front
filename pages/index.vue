<template>
  <div class="h-screen w-full flex items-center justify-center">
    <div class="bg-white w-[25%] border flex items-center justify-center flex-col gap-5 p-2 py-4 rounded-md">
      <h1 class="font-medium text-gray-600">Welcome To My App</h1>
      <ElButton type="success" class="w-full">Click Here To Detail</ElButton>
    </div>
  </div>
</template>

<script lang="ts" setup>
  const items: any = ref([]);
  const handleGetUser = async()=>{
    try {
      const response = await $fetch('http://www.myapp.me/api/user', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
      });
      items.value = response;
    }catch(error){
      console.log(error);
    }
  }

  onMounted(()=>{
    handleGetUser();
  })
</script>

<style>

</style>