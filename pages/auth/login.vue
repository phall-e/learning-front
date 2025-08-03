<template>
  <div class="h-screen w-full flex items-center justify-center">
    <ElForm
      class="w-[25%] border rounded-md p-4"
      label-position="top"
      @submit.prevent="handleLogin"
    >
    <h1 align="center" class=" text-[20px]">Login</h1>
      <ElFormItem label="Username">
        <ElInput v-model="formData.username" placeholder="Username" clearable>
          <template #prefix>
            <Icon name="mynaui:user"/>
          </template>
        </ElInput>
      </ElFormItem>
      <ElFormItem label="Password">
        <ElInput v-model="formData.password" type="password" placeholder="Password" clearable show-password>
          <template #prefix>
            <Icon name="material-symbols-light:lock-outline-sharp"/>
          </template>
        </ElInput>
      </ElFormItem>
      <ElFormItem>
        <ElButton type="success" class="w-full" native-type="submit">
          <Icon v-if="loading" name="eos-icons:bubble-loading"/>
          <span v-else>Login</span>
        </ElButton>
      </ElFormItem>
    </ElForm>
  </div>
</template>

<script lang="ts" setup>
  definePageMeta({
    layout: 'auth',
  });

  const formData = reactive({
    username: '',
    password: ''
  });

  const loading = ref(false);

  const handleLogin = async() =>{
    loading.value = true;
    try {
      const response = await $fetch('http://localhost:8000/api/auth/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: formData,
      });
      ElMessage.success('Successfully')
      navigateTo('/');
    } catch (error: any) {
      loading.value = false;
      console.log(error);
      ElMessage.error('Unauthorization')
    } finally {
      loading.value = false;
      
    }
  }
</script>
