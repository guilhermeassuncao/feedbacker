<template>
    <header class="flex justify-center w-full h-28 bg-brand-main">
        <header-logged />
    </header>
    <div class="flex flex-col items-center justify-center h-64 bg-brand-gray">
        <h1 class="text-4xl font-black text-center text-gray-800">Feedbacks</h1>
        <p class="text-lg text-center text-gray-800 font-regular">
            Detalhes de todos os feedbacks recebidos.
        </p>
    </div>
    <div class="flex justify-center w-full pb-20">
        <div class="w-4/5 max-w-6xl py-10 grid grid-cols-4 gap-2">
            <div class="col-span-1">
                <h1 class="text-3xl font-black text-brand-darkgray">
                    Listagem
                </h1>
                <suspense>
                    <template #default>
                        <filters
                            class="mt-8 animate__animated animate__fadeIn animate__faster"
                        />
                    </template>
                    <template #fallback>
                        <filters-loading class="mt-8" />
                    </template>
                </suspense>
            </div>
            <div class="col-span-3 px-10 pt-20">
                <p
                    v-if="state.hasError"
                    class="text-lg text-center text-gray-800 font-regular"
                >
                    Aconteceu um erro ao carregar os feedbacks
                </p>

                
                <p
                    v-if="!state.feedbacks.length && !state.isLoading"
                    class="text-lg text-center text-gray-800 font-regular"
                >
                    Ainda nenhum feedback recebido

                    {{!state.feedbacks.length}}
                    {{!state.isLoading}}
                </p>

                <feedback-card-loading v-if="state.isLoading" />

                <feedback-card
                    v-else
                    v-for="(feedback, index) in state.feedback"
                    :key="feedback.id"
                    :is-open="index === 0"
                    :feedback="feedback"
                    class="mb-8"
                />
            </div>
        </div>
    </div>
</template>

<script>
import { reactive, onMounted } from "vue";
import HeaderLogged from "../../components/HeaderLogged";
import Filters from "./Filters";
import FiltersLoading from "./FiltersLoading";
import FeedbackCard from "../../components/FeedbackCard";
import FeedbackCardLoading from "../../components/FeedbackCard/Loading";
import services from "../../services";

export default {
    components: {
        HeaderLogged,
        Filters,
        FiltersLoading,
        FeedbackCard,
        FeedbackCardLoading,
    },
    setup() {
        const state = reactive({
            feedbacks: [],
            isLoading: false,
            currentFeedbackType: "",
            pagination: {
                limit: 5,
                offset: 0,
            },
            hasError: false,
        });

        function handleErrors(error) {
            state.hasError = !!error;
        }

        onMounted(() => {
            fetchFeedbacks();
        });

        async function fetchFeedbacks() {
            try {
                state.isLoading = true;

                const { data } = await services.feedbacks.getAll({
                    ...state.pagination,
                    type: state.currentFeedbackType,
                });

                state.feedback = data.results;
                state.pagination = data.pagination;
                state.isLoading = false;
            } catch (error) {
                handleErrors(error);
            }
        }

        return {
            state,
            fetchFeedbacks,
        };
    },
};
</script>

<style></style>
