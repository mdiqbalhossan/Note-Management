<script setup>
import { ref } from "vue";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head, Link, useForm } from "@inertiajs/inertia-vue3";
import BackButton from "@/Components/BackButton.vue";
import InputError from "@/Components/InputError.vue";
import TextInput from "@/Components/forms/TextInput.vue";
import Label from "@/Components/forms/Label.vue";
const props = defineProps({
    student: {
        type: Object,
        default: () => ({}),
    },
});

const form = useForm({
    name: props.student?.name,
    phone: props.student?.phone,
    email: props.student?.email,
    college_name: props.student?.college_name,
    address: props.student?.address,
    username: props.student?.username,
    password: props.student?.password,
    status: props.student?.status == 1 ? "true" : "false",
});
const submit = () => {
    form.put(route("student.update", props.student?.id));
};
const login_details = ref(false);
</script>
<template>
    <Head title="Class Edit" />
    <AuthenticatedLayout>
        <div
            class="w-full max-w-md bg-white border mx-auto my-5 border-gray-200 rounded-lg shadow-md sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700"
        >
            <form class="space-y-6" @submit.prevent="submit">
                <h5 class="text-xl font-medium text-gray-900 dark:text-white">
                    Edit Class
                    <BackButton :url="route('class.index')" />
                </h5>
                <div>
                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <Label value="Student Name" id="name" req="true" />

                            <TextInput
                                id="name"
                                type="text"
                                v-model="form.name"
                                required
                                autofocus
                                autocomplete="name"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.name"
                            />
                        </div>
                        <div>
                            <Label
                                value="Contact No"
                                id="contact_no"
                                req="true"
                            />

                            <TextInput
                                id="contact_no"
                                type="text"
                                v-model="form.phone"
                                required
                                autofocus
                                autocomplete="phone"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.phone"
                            />
                        </div>
                        <div>
                            <Label value="Email" id="email" />

                            <TextInput
                                id="email"
                                type="email"
                                v-model="form.email"
                                autofocus
                                autocomplete="email"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.email"
                            />
                        </div>
                        <div>
                            <Label value="College Name" id="college_name" />

                            <TextInput
                                id="college_name"
                                type="text"
                                v-model="form.college_name"
                                autofocus
                                autocomplete="college_name"
                            />
                            <InputError
                                class="mt-2"
                                :message="form.errors.college_name"
                            />
                        </div>
                    </div>
                    <div>
                        <Label value="Address" id="address" />

                        <TextInput
                            id="address"
                            type="text"
                            v-model="form.address"
                            autofocus
                            autocomplete="address"
                        />
                        <InputError
                            class="mt-2"
                            :message="form.errors.address"
                        />
                    </div>
                </div>

                <div class="flex items-start">
                    <div class="flex items-start">
                        <div class="flex items-center h-5">
                            <input
                                id="login_details"
                                type="checkbox"
                                value=""
                                class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800"
                                v-model="login_details"
                            />
                        </div>

                        <Label
                            value="Student Login Details"
                            id="login_details"
                            customClass="ml-2"
                        />
                    </div>
                </div>

                <!-- Login Details -->
                <div class="grid grid-cols-2 gap-2" v-if="login_details">
                    <div>
                        <Label value="Username" id="username" />

                        <TextInput
                            id="username"
                            type="text"
                            v-model="form.username"
                            autofocus
                            autocomplete="username"
                        />
                        <InputError
                            class="mt-2"
                            :message="form.errors.username"
                        />
                    </div>
                    <div>
                        <Label value="Password" id="password" />

                        <TextInput
                            id="password"
                            type="password"
                            v-model="form.password"
                            autofocus
                            autocomplete="password"
                        />
                        <InputError
                            class="mt-2"
                            :message="form.errors.password"
                        />
                    </div>
                </div>
                <!-- Login Details -->

                <div class="flex items-start">
                    <div class="flex items-start">
                        <div class="flex items-center h-5">
                            <input
                                id="remember"
                                type="checkbox"
                                value=""
                                class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-blue-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-blue-600 dark:ring-offset-gray-800"
                                v-model="form.status"
                            />
                        </div>

                        <Label
                            value="Publish"
                            id="remember"
                            customClass="ml-2"
                        />
                    </div>
                </div>
                <button
                    type="submit"
                    class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                    :class="{ 'opacity-25': form.processing }"
                    :disabled="form.processing"
                >
                    Update
                </button>
            </form>
        </div>
    </AuthenticatedLayout>
</template>
