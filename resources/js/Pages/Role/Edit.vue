<template>
    <app-layout>
        <template #header>
            <div class="flex flex-row">
                <a :href="route('roles.index')">
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="h-6 w-6 text-white"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M15 19l-7-7 7-7"
                        />
                    </svg>
                </a>
                <h2 class="font-semibold text-xl text-white leading-tight">
                    Create role
                </h2>
            </div>
        </template>
        <div class="py-4">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <breeze-validation-errors class="mb-4" />
                        <form @submit.prevent="submit">
                            <div class="grid grid-cols-1 sm:grid-cols-1 mt-4">
                                <div>
                                    <label class="text-gray-700" for="rolename"
                                        >Name
                                    </label>
                                    <input
                                        class="w-full mt-2 rounded-md focus:border-indigo-600"
                                        type="text"
                                        v-model="form.name"
                                    />
                                </div>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-1 mt-4">
                                <div>
                                    <label
                                        class="text-gray-700"
                                        for="permission"
                                    >
                                        Permissions
                                    </label>
                                    <select
                                        multiple
                                        v-model="form.permissions"
                                        class="mt-2 appearance-none rounded border block appearance-none w-full bg-white border-gray-400 text-gray-700 py-2 px-4 pr-8 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                                    >
                                        <option
                                            v-for="permission in permissions"
                                            :key="permission.id"
                                            :value="permission.name"
                                        >
                                            {{ permission.name }}
                                        </option>
                                    </select>
                                </div>
                            </div>
                            <div class="flex justify-end mt-4">
                                <button
                                    class="px-4 py-2 bg-gray-800 text-gray-200 rounded-md hover:bg-gray-700 focus:outline-none focus:bg-gray-700"
                                >
                                    Save
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </app-layout>
</template>
<script>
import BreezeValidationErrors from "@/Components/ValidationErrors";
import AppLayout from "@/Layouts/Backend/Default";
export default {
    components: {
        AppLayout,
        BreezeValidationErrors,
    },
    props: {
        role: {
            type: Object,
        },
        permissions: {
            type: Array,
        },
    },
    data() {
        return {
            form: this.$inertia.form({
                name: this.role.name,
                permissions: this.role.permission_names,
            }),
        };
    },
    methods: {
        submit() {
            this.form.put(route("roles.update", { id: this.role.id }));
        },
    },
};
</script>
<style></style>
