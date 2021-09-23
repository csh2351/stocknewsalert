<template>
    <Head title="Log in"/>

    <div class="hidden fixed top-0 right-0 px-6 py-4 sm:block">
        <Link :href="route('register')" class="ml-4 text-sm text-gray-900 underline">
            Register
        </Link>
    </div>

    <BreezeValidationErrors class="mb-4"/>

    <div class="mb-4 font-medium text-sm text-green-600" v-if="status">
        {{ status }}
    </div>

    <form @submit.prevent="submit">
        <div>
            <BreezeLabel for="email" value="Email"/>
            <BreezeInput autocomplete="username" autofocus class="mt-1 block w-full" id="email" required type="email" v-model="form.email"/>
        </div>

        <div class="mt-4">
            <BreezeLabel for="password" value="Password"/>
            <BreezeInput autocomplete="current-password" class="mt-1 block w-full" id="password" required type="password" v-model="form.password"/>
        </div>

        <div class="block mt-4">
            <label class="flex items-center">
                <BreezeCheckbox name="remember" v-model:checked="form.remember"/>
                <span class="ml-2 text-sm text-gray-600">Remember me</span>
            </label>
        </div>

        <div class="flex items-center justify-end mt-4">
            <Link :href="route('password.request')" class="underline text-sm text-gray-600 hover:text-gray-900" v-if="canResetPassword">
                Forgot your password?
            </Link>

            <BreezeButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing" class="ml-4">
                Log in
            </BreezeButton>
        </div>
    </form>
</template>

<script>
    import BreezeButton from '@/Components/Button.vue'
    import BreezeCheckbox from '@/Components/Checkbox.vue'
    import BreezeGuestLayout from '@/Layouts/Guest.vue'
    import BreezeInput from '@/Components/Input.vue'
    import BreezeLabel from '@/Components/Label.vue'
    import BreezeValidationErrors from '@/Components/ValidationErrors.vue'
    import {Head, Link} from '@inertiajs/inertia-vue3';

    export default {
        layout: BreezeGuestLayout,

        components: {
            BreezeButton,
            BreezeCheckbox,
            BreezeInput,
            BreezeLabel,
            BreezeValidationErrors,
            Head,
            Link,
        },

        props: {
            canResetPassword: Boolean,
            status: String,
        },

        data() {
            return {
                form: this.$inertia.form({
                    email: '',
                    password: '',
                    remember: false
                })
            }
        },

        methods: {
            submit() {
                this.form.post(this.route('login'), {
                    onFinish: () => this.form.reset('password'),
                })
            }
        }
    }
</script>
