<script setup>
import BreezeButton from '@/Components/Button.vue';
import BreezeCheckbox from '@/Components/Checkbox.vue';
import BreezeGuestLayout from '@/Layouts/Guest.vue';
import BreezeInput from '@/Components/Input.vue';
import BreezeInputError from '@/Components/InputError.vue';
import BreezeLabel from '@/Components/Label.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: '',
    password: '',
    remember: false
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <BreezeGuestLayout class="container">
        <Head title="Iniciar Sesión" />

        <div v-if="status" class="mb-4">
            {{ status }}
        </div>

        <div class="row">
            <div class="col-12 col-md-6 m-auto">
                <div class="card p-4">
                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <BreezeLabel for="email" value="Correo Electrónico" class="form-label"/>
                            <BreezeInput id="email" type="email" class="form-control" v-model="form.email" required autofocus autocomplete="username" />
                            <BreezeInputError class="mt-2" :message="form.errors.email" />
                        </div>

                        <div class="mb-3">
                            <BreezeLabel for="password" value="Contraseña" class="form-label"/>
                            <BreezeInput id="password" type="password" class="form-control" v-model="form.password" required autocomplete="current-password" />
                            <BreezeInputError class="mt-2" :message="form.errors.password" />
                        </div>

                        <div class="form-check">
                            <BreezeCheckbox name="remember" v-model:checked="form.remember" class="form-check-input"/>
                            <label class="form-check-label" for="flexCheckDefault">Recuerdame</label>
                        </div>

                        <div class="d-flex align-items-center justify-content-end gap-4">
                            <Link v-if="canResetPassword" :href="route('password.request')" class="underline text-sm text-gray-600 hover:text-gray-900">
                                Forgot your password?
                            </Link>

                            <BreezeButton class="btn btn-dark" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                                Log in
                            </BreezeButton>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </BreezeGuestLayout>
</template>
