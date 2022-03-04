<template>
    <custom-header @create-account="handleAccountCreate" @login="handleLogin" />
    <contact />
    <footer class="flex justify-center py-6 bg-brand-main shadow-sm">
        <p class="text-center font-medium text-gray-100">
            © 2022 Feedback, All rights reserved.
        </p>
    </footer>
</template>
<script>
import CustomHeader from "./CustomHeader.vue";
import Contact from "./Contact.vue";
import { useRouter } from 'vue-router';
import { onMounted } from '@vue/runtime-core';

export default {
    components: {
        CustomHeader,
        Contact,
    },
    setup() {
        const router = useRouter();

        onMounted(() => {
            const token = window.localStorage.getItem("token");

            if (token) {
                router.push({name: "Feedbacks"});
            }
        });
        function handleAccountCreate() {}

        function handleLogin() {}

        return {
            handleAccountCreate,
            handleLogin,
        };
    },
};
</script>
<style></style>
