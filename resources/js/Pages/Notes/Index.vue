<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { Head, Link } from '@inertiajs/vue3';
import { router } from '@inertiajs/vue3'
import { ref, watch } from "vue";

defineProps({notes: Array});

const valor = ref(null);

const search = () => {
    let q= valor.value;
    console.log('Search for: ', q);
    router.get(route('notes.index', {q}), {}, {preserveState: true});
};
</script>

<template>
    <AppLayout title="Notes">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Notes module
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="md:grid md:grid-cols-3 md:gap-6">
                    <div class="md:col-span-1">
                        <div class="px-4 sm:px0">
                            <h3 class="text-lg text-gray-900">Notes list</h3>
                            <p class="text-sm text-gray-600">Select the correct record and run any function (view, edit or delete)</p>
                        </div>
                    </div>
                    <div class="md:col-span-2 mt-5 md:mt-0">
                        <div class="shadow bg-white md:rounded p-4">
                            <div class="flex justify-between">
                                <input type="text"
                                    class="form-input rounded-md shadow-sm"
                                    placeholder="search..."
                                    v-model="valor" @keyup="search">
                                <Link :href="route('notes.create')"
                                    class="bg-blue-500  font-bold px-4 py-2 rounded">
                                    Create
                                </Link>
                            </div>
                            <hr class="my-6" />
                            <table>
                                <tr v-for="note in notes">
                                    <td class="border px-4 py-2">
                                        {{ note.excerpt }}
                                    </td>
                                    <td class="px-4 py-2">
                                        <Link :href="route('notes.show', note.id)">
                                            Show
                                        </Link >
                                    </td>
                                    <td class="px-4 py-2">
                                        <Link :href="route('notes.edit', note.id)">
                                            Edit
                                        </Link>
                                    </td>
                                </tr>
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
