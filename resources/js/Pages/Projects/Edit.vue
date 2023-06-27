<template>
    <Head title="Project" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Create Project</h2>
        </template>

        <div class="py-4">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <form @submit.prevent="submit">
                    <div>
                        <InputLabel for="name" value="Name" />

                        <TextInput id="name" type="text" class="mt-1 block w-full" v-model="form.name" required autofocus
                            autocomplete="username" />

                        <InputError class="mt-2" :message="$page.props.errors.name" />
                    </div>
                    <div>
                        <InputLabel for="project_url" value="URL" />

                        <TextInput id="prject_url" type="text" class="mt-1 block w-full" v-model="form.project_url" required autofocus
                            autocomplete="projecturl" />

                        <InputError class="mt-2" :message="$page.props.errors.project_url" />
                    </div>
                    <div>
                        <InputLabel for="skill_id" value="Skill" />
                        <select v-model="form.skill_id" id="skill_id" name="skill_id">
                            <option v-for="skill in skills" :key="skill.id" :value="skill.id" class="mt-1 block w-full">{{ skill.name  }}</option>
                        </select>
                        <InputError class="mt-2" :message="$page.props.errors.skill_id" />
                    </div>
                    <div>
                        <InputLabel for="image" value="Image" />

                        <TextInput id="image" type="file" class="mt-1 block w-full"
                            @input="form.image = $event.target.files[0]" />

                        <InputError class="mt-2" :message="$page.props.errors.image" />
                    </div>


                    <div class="flex items-center justify-end mt-4">
                        <PrimaryButton class="ml-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                            Store
                        </PrimaryButton>
                    </div>
                </form>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Checkbox from '@/Components/Checkbox.vue';

import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
import {Inertia} from "@inertiajs/inertia";

const props=defineProps({
    skills: Array,
    project: Object,
})

const form = useForm({
    name: props.project?.name,
    skill_id: props.project?.skill_id,
    project_url: props.project.project_url,
    image: null,
});

const submit = () => {
    Inertia.post(`/projects/${props.project.id}`, {
        _method: "put",
        name: form.name,
        skill_id: form.skill_id,
        project_url: form.project_url,
        image: form.image,
    })
};
</script>
    
<style></style>