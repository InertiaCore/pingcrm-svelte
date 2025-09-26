<script>
    import { router } from '@inertiajs/svelte';
    import {page} from '@inertiajs/svelte';
    import { onMount } from 'svelte';
    import GuestLayout from '@/Shared/GuestLayout.svelte';
    import LoadingButton from '@/Shared/LoadingButton.svelte';
    import TextInput from '@/Shared/TextInput.svelte';
    import Helmet from '@/Shared/Helmet.svelte';

    $: errors = $page?.errors || {};

    let sending = false;
    let formVisible = false;
    let values = {
        email: 'johndoe@example.com',
        password: 'secret',
        remember: true
    };

    onMount(() => {
        setTimeout(() => {
            formVisible = true;
        }, 100);
    });

    function handleChange(e) {
        const key = e.target.name;
        const value =
            e.target.type === 'checkbox' ? e.target.checked : e.target.value;

        values = {
            ...values,
            [key]: value
        };
    }

    function handleSubmit() {
        sending = true;
        router.post('/login', values).then(() => {
            sending = false;
        }).catch(() => {
            sending = false;
        });
    }
</script>

<Helmet title="Login"/>

<GuestLayout>
    <form
        on:submit|preventDefault={handleSubmit}
        class="bg-white rounded-2xl shadow-2xl overflow-hidden backdrop-blur-sm transition-all duration-500 hover:shadow-3xl transform
               {formVisible ? 'translate-y-0 opacity-100' : 'translate-y-8 opacity-0'}
               {sending ? 'scale-[0.98]' : 'scale-100'}"
    >
            <div class="px-10 py-12">
                <div class="text-center mb-8">
                    <h1 class="text-3xl font-bold bg-gradient-to-r from-indigo-600 to-purple-600 bg-clip-text text-transparent">
                        Welcome Back!
                    </h1>
                    <p class="text-gray-600 mt-2">Please sign in to your account</p>
                    <div class="mx-auto mt-4 w-20 h-1 bg-gradient-to-r from-indigo-500 to-purple-500 rounded-full"></div>
                </div>

                <div class="space-y-6">
                    <TextInput
                        label="Email Address"
                        name="email"
                        type="email"
                        errors={errors.email}
                        value={values.email}
                        onChange={handleChange}
                    />

                    <TextInput
                        label="Password"
                        name="password"
                        type="password"
                        errors={errors.password}
                        value={values.password}
                        onChange={handleChange}
                    />

                    <div class="flex items-center justify-between">
                        <label class="flex items-center cursor-pointer group" for="remember">
                            <input
                                name="remember"
                                id="remember"
                                type="checkbox"
                                checked={values.remember}
                                on:change={handleChange}
                                class="w-4 h-4 text-indigo-600 bg-gray-100 border-gray-300 rounded focus:ring-indigo-500 focus:ring-2 transition-colors"
                            />
                            <span class="ml-3 text-sm text-gray-700 group-hover:text-indigo-600 transition-colors">
                                Remember me
                            </span>
                        </label>

                        <a
                            href="#reset-password"
                            class="text-sm text-indigo-600 hover:text-indigo-500 transition-colors hover:underline"
                        >
                            Forgot password?
                        </a>
                    </div>
                </div>
            </div>

            <div class="px-10 py-6 bg-gradient-to-r from-gray-50 to-gray-100 border-t border-gray-200">
                <LoadingButton
                    type="submit"
                    loading={sending}
                    className="w-full"
                >
                    Sign In
                </LoadingButton>
            </div>
    </form>
</GuestLayout>
