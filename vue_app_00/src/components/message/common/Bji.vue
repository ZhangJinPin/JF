<template>
    <mt-header title="修改" class="tb">
        <router-link to="" slot="left">
            <mt-button icon="back" @click="$router.back(-1)">返回</mt-button>
        </router-link>
    </mt-header>
</template>

<style scoped>
    .tb{
        height: 48px;
        font-size:18px; 
    }
</style>