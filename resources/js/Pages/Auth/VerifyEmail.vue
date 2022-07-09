<script setup>
import { computed } from 'vue';
import BreezeButton from '@/Components/Button.vue';
import BreezeGuestLayout from '@/Layouts/Guest.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

const props = defineProps({
    status: String,
});

const form = useForm();

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');
</script>

<template>
    <BreezeGuestLayout>
        <Head title="אימות דואר אלקטרוני" />

        <div class="mb-4 text-sm text-gray-600">
            תודה על ההרשמה! לפני שתתחיל, האם תוכל לאמת את כתובת הדוא"ל שלך על ידי לחיצה על הקישור שזה עתה שלחנו לך בדוא"ל? אם לא קיבלת את המייל, נשלח לך בשמחה דוא"ל נוסף.
        </div>

        <div class="mb-4 font-medium text-sm text-green-600" v-if="verificationLinkSent" >
            קישור אימות חדש נשלח לכתובת האימייל שסיפקת במהלך ההרשמה.
        </div>

        <form @submit.prevent="submit">
            <div class="mt-4 flex items-center justify-between">
                <BreezeButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    שלחו לי דוא"ל לאימות
                </BreezeButton>

                <Link :href="route('logout')" method="post" as="button" class="underline text-sm text-gray-600 hover:text-gray-900">התנתק</Link>
            </div>
        </form>
    </BreezeGuestLayout>
</template>
