<script setup>
import BreezeButton from '@/Components/Button.vue';
import BreezeGuestLayout from '@/Layouts/Guest.vue';
import BreezeInput from '@/Components/Input.vue';
import BreezeLabel from '@/Components/Label.vue';
import BreezeValidationErrors from '@/Components/ValidationErrors.vue';
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
    <BreezeGuestLayout>
        <Head title="שכחתי סיסמא" />

        <div class="mb-4 text-sm text-gray-600">
            שכחת סיסמא? אין בעיה. פשוט הודע לנו על כתובת הדוא"ל שלך ואנו נשלח לך באימייל קישור לאיפוס סיסמה שיאפשר לך לבחור סיסמא חדשה.
        </div>

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <BreezeValidationErrors class="mb-4" />

        <form @submit.prevent="submit">
            <div>
                <BreezeLabel for="email" value="דואר אלקטרוני" />
                <BreezeInput id="email" type="email" class="mt-1 block w-full" v-model="form.email" required autofocus autocomplete="username" />
            </div>

            <div class="flex items-center justify-end mt-4">
                <BreezeButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    שלחו לי מייל עם כתובת לאיפוס סיסמא
                </BreezeButton>
            </div>
        </form>
    </BreezeGuestLayout>
</template>
