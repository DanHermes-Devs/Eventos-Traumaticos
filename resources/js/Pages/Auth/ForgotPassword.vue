<script setup>
import BreezeButton from '@/Components/Button.vue';
import BreezeGuestLayout from '@/Layouts/Guest.vue';
import BreezeInput from '@/Components/Input.vue';
import BreezeInputError from '@/Components/InputError.vue';
import BreezeLabel from '@/Components/Label.vue';
import { Head, useForm } from '@inertiajs/inertia-vue3';

defineProps({
    status: String,
});

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <BreezeGuestLayout class="container">
        <Head title="Forgot Password" />
        <div class="row">
            <div class="col-12 col-md-6 m-auto">
                <div class="card p-3">
                    <div class="mb-4">
                        ¿Ha olvidado su contraseña? No hay problema. Sólo tienes que indicarnos tu dirección de correo electrónico y te enviaremos un enlace para restablecer la contraseña que te permitirá elegir una nueva.
                    </div>

                    <div v-if="status" class="mb-4">
                        {{ status }}
                    </div>

                    <form @submit.prevent="submit">
                        <div class="mb-3">
                            <BreezeLabel for="email" value="Email" class="form-label"/>
                            <BreezeInput id="email" type="email" class="form-control" v-model="form.email" required autofocus autocomplete="username" />
                            <BreezeInputError class="mt-2" :message="form.errors.email" />
                        </div>

                        <div class="d-flex align-items-center justify-content-end">
                            <BreezeButton class="btn btn-dark" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                                Enlace para restablecer la contraseña por correo electrónico
                            </BreezeButton>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </BreezeGuestLayout>
</template>
