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
import { onMounted } from "vue";
import { useRouter } from "vue-router";
import CustomHeader from "./CustomHeader.vue";
import Contact from "./Contact.vue";
import useModal from "../../hooks/useModal";

export default {
    components: {
        CustomHeader,
        Contact,
    },
    setup() {
        const router = useRouter();
        const modal = useModal();

        onMounted(() => {
            const token = window.localStorage.getItem("token");

            if (token) {
                router.push({ name: "Feedbacks" });
            }
        });
        function handleAccountCreate() {
            modal.open({
                component: "ModalCreateAccount",
            });
        }

        function handleLogin() {
            modal.open({
                component: "ModalLogin",
            });
        }

        return {
            handleAccountCreate,
            handleLogin,
        };
    },
};
</script>
<style></style>
