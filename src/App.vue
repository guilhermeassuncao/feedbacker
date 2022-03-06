<template>
    <modal-factory />
    <router-view />
</template>
<script>
import ModalFactory from "../src/components/ModalFactory";

export default {
    components: { ModalFactory },
};
</script>
