<script setup>
import { reactive } from "vue";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head, Link } from "@inertiajs/inertia-vue3";
import Alert from "@/Components/Alert.vue";
import Paginate from "@/Components/Paginate.vue";
import Icon from "@/Components/Icon.vue";
import DeleteModal from "@/Components/DeleteModal.vue";
defineProps({
    students: Object,
});
const data = reactive({
    show: false,
    id: "",
});
const destroy = (student_id) => {
    data.show = true;
    data.id = student_id;
};
</script>
<template>
    <Head title="Student" />
    <AuthenticatedLayout>
        <DeleteModal
            v-model="data.show"
            :id="data.id"
            route="student.destroy"
        />
        <div class="p-2 my-4">
            <div
                v-if="$page.props.flash.message"
                class="w-full max-w-md mx-auto"
            >
                <Alert />
            </div>
            <div class="overflow-x-auto relative shadow-md sm:rounded-lg">
                <div
                    class="p-4 bg-white dark:bg-gray-900 flex flex-wrap items-center justify-between"
                >
                    <label for="table-search" class="sr-only">Search</label>
                    <div class="relative mt-1">
                        <div
                            class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none"
                        >
                            <Icon
                                path="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
                            />
                        </div>
                        <input
                            type="text"
                            id="table-search"
                            class="block p-2 pl-10 w-80 text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Search for items"
                        />
                    </div>
                    <Link
                        :href="route('student.create')"
                        type="button"
                        class="text-white bg-gradient-to-r from-green-400 via-green-500 to-green-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-green-300 dark:focus:ring-green-800 shadow-lg shadow-green-500/50 dark:shadow-lg dark:shadow-green-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2"
                    >
                        Add Student
                    </Link>
                </div>
                <table
                    class="w-full text-sm text-left text-gray-500 dark:text-gray-400"
                >
                    <thead
                        class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
                    >
                        <tr>
                            <th scope="col" class="py-3 px-6">SI</th>
                            <th scope="col" class="py-3 px-6">Name</th>
                            <th scope="col" class="py-3 px-6">Phone</th>
                            <th scope="col" class="py-3 px-6">Unique ID</th>
                            <th scope="col" class="py-3 px-6">Status</th>
                            <th scope="col" class="py-3 px-6">Action</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                            class="bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600"
                            v-for="student in students.data"
                            :key="student.id"
                        >
                            <th
                                scope="row"
                                class="py-4 px-6 font-medium text-gray-900 whitespace-nowrap dark:text-white"
                            >
                                {{ student.id }}
                            </th>
                            <td class="py-4 px-6">{{ student.name }}</td>
                            <td class="py-4 px-6">{{ student.phone }}</td>
                            <td class="py-4 px-6">{{ student.unique_id }}</td>
                            <td class="py-4 px-6">
                                {{
                                    student.status == 1
                                        ? "Published"
                                        : "Pending"
                                }}
                            </td>
                            <td class="py-4 px-6">
                                <Link
                                    :href="route('student.edit', student.id)"
                                    as="button"
                                    class="bg-indigo-600 hover:bg-indigo-800 px-1 py-1 rounded-md text-white font-semibold tracking-wide cursor-pointer"
                                >
                                    <Icon
                                        path="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z"
                                    />
                                </Link>

                                <Link
                                    :href="route('student.edit', student.id)"
                                    as="button"
                                    class="bg-teal-600 hover:bg-teal-800 px-1 py-1 mx-2 rounded-md text-white font-semibold tracking-wide cursor-pointer"
                                >
                                    <svg
                                        class="w-6 h-6"
                                        fill="currentColor"
                                        viewBox="0 0 20 20"
                                        xmlns="http://www.w3.org/2000/svg"
                                    >
                                        <path
                                            d="M10 12a2 2 0 100-4 2 2 0 000 4z"
                                        ></path>
                                        <path
                                            fill-rule="evenodd"
                                            d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z"
                                            clip-rule="evenodd"
                                        ></path>
                                    </svg>
                                </Link>

                                <Link
                                    :href="route('student.edit', student.id)"
                                    as="button"
                                    class="bg-indigo-600 hover:bg-indigo-800 px-1 py-1 rounded-md text-white font-semibold tracking-wide cursor-pointer"
                                >
                                    <Icon
                                        path="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10"
                                    />
                                </Link>
                                <button
                                    @click="destroy(student.id)"
                                    type="button"
                                    class="bg-red-600 hover:bg-red-800 px-1 py-1 mx-2 rounded-md text-white font-semibold tracking-wide cursor-pointer"
                                >
                                    <Icon
                                        path="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
                                    />
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <div class="p-2">
                    <Paginate :data="students" />
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
