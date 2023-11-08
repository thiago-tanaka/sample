<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import {Head, Link} from '@inertiajs/vue3';
import {ref} from "vue";

const usersFromApiGateway = ref();

axios.get('https://yw13ttiv75.execute-api.ap-northeast-1.amazonaws.com/v1/get-from-js-lambda').then((response) => {
    console.log(response.data);
    usersFromApiGateway.value = response.data;
    return response.data;
});

console.log('usersFromApiGateway', usersFromApiGateway)

defineProps({
    users: {
        type: Array,
    },
});

// const kanjis2 = axios.get('https://yw13ttiv75.execute-api.ap-northeast-1.amazonaws.com/v1/get-kanjis').then((response) => {
//     console.log('kanjis', response.data);
//     return response.data;
// });

</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900">You're logged in!</div>

                    <div class="p-6 text-gray-900">
                        <h1>users from local</h1>
                        <div v-for="user in users">
                            {{user.name}}
                        </div>
                    </div>

                    <div class="p-6 text-gray-900">
                        <h1>users from api gateway</h1>
                        <div v-for="user in usersFromApiGateway">
                            {{user.name}}
                        </div>
                    </div>

                    <div class="p-6 text-gray-900">
                        <Link
                            :href="route('users.create')"
                            class="text-sm text-gray-700 underline"
                        >Create User</Link
                        >
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
