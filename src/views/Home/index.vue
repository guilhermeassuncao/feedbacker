<template>
    <custom-header />
    <contact />
    <footer class="flex justify-center py-6 bg-brand-main shadow-sm">
        <p class="text-center font-medium text-gray-100">© 2022 Feedback, All rights reserved.</p>
    </footer>
</template>
<script>
import CustomHeader from './CustomHeader.vue'
import Contact from './Contact.vue'

export default {
    components: {
        CustomHeader,
        Contact
    }
};
</script>
<style></style>
