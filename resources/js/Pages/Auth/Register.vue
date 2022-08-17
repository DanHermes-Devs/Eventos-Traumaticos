<script setup>
import BreezeButton from '@/Components/Button.vue';
import BreezeGuestLayout from '@/Layouts/Guest.vue';
import BreezeInput from '@/Components/Input.vue';
import BreezeInputError from '@/Components/InputError.vue';
import BreezeLabel from '@/Components/Label.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
    terms: false,
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <BreezeGuestLayout class="container">
        <Head title="Registro" />
        <div class="row">
            <div class="col-12 col-md-6 m-auto">
                <div class="card p-3">
                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <BreezeLabel for="name" value="Name" class="form-label"/>
                            <BreezeInput id="name" type="text" class="form-control" v-model="form.name" required autofocus autocomplete="name" />
                            <BreezeInputError class="mt-2" :message="form.errors.name" />
                        </div>

                        <div class="mb-3">
                            <BreezeLabel for="email" value="Email" class="form-label"/>
                            <BreezeInput id="email" type="email" class="form-control" v-model="form.email" required autocomplete="username" />
                            <BreezeInputError class="mt-2" :message="form.errors.email" />
                        </div>

                        <div class="mb-3">
                            <BreezeLabel for="password" value="Password" class="form-label"/>
                            <BreezeInput id="password" type="password" class="form-control" v-model="form.password" required autocomplete="new-password" />
                            <BreezeInputError class="mt-2" :message="form.errors.password" />
                        </div>

                        <div class="mb-3">
                            <BreezeLabel for="password_confirmation" value="Confirm Password" class="form-label" />
                            <BreezeInput id="password_confirmation" type="password" class="form-control" v-model="form.password_confirmation" required autocomplete="new-password" />
                            <BreezeInputError class="mt-2" :message="form.errors.password_confirmation" />
                        </div>

                        <div class="d-flex align-items-center justify-content-end gap-3">
                            <Link :href="route('login')" class="underline text-sm text-gray-600 hover:text-gray-900">
                                Already registered?
                            </Link>

                            <BreezeButton class="btn btn-dark" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                                Registrate
                            </BreezeButton>
                        </div>
                    </form>

                </div>
            </div>
        </div>
    </BreezeGuestLayout>
</template>
