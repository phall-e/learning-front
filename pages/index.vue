<template>
  <div class="flex items-center h-screen flex-col justify-center">
    <h1>User Information</h1>
   <ElTable
    :data="items"
    stripe
   >
    <ElTableColumn type="index"/>
    <el-table-column label="Username" prop="username"/>
    <el-table-column label="Email" prop="email"/>
    <el-table-column label="Created At" prop="createdAt"/>

    <el-table-column label="Action" width="150">
      <template #default="scope">
        <div class="flex items-center justify-center gap-2">
          <el-tag type="primary">
            <Icon name="solar:eye-linear"/>
          </el-tag>
          <el-tag type="success">
            <Icon name="akar-icons:edit"/>
          </el-tag>
          <el-tag type="danger">
            <Icon name="akar-icons:edit"/>
          </el-tag>
        </div>
      </template>
    </el-table-column>

   </ElTable>
  </div>
</template>

<script lang="ts" setup>
  const items: any = ref([]);
  const handleGetUser = async()=>{
    try {
      const response = await $fetch('http://localhost:8000/api/user', {
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