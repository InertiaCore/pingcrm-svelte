<script>
    export let onChange;
    export let label;
    export let name;
    export let className = '';
    export let errors = [];
    export let type = 'text';
    export let value = '';

    let focused = false;
    let input;

    $: props = (({ onChange, label, name, className, errors, type, value, ...rest }) => rest)($$props);
    $: hasError = errors && errors.length > 0;
    $: hasValue = value && value.toString().length > 0;
</script>

<div class="input-group {className}">
    <div class="relative">
        <input
            bind:this={input}
            bind:value
            id={name}
            name={name}
            {type}
            {...props}
            on:change={onChange}
            on:focus={() => focused = true}
            on:blur={() => focused = false}
            class="peer w-full px-4 py-3 bg-white border-2 rounded-lg text-gray-900 placeholder-transparent transition-all duration-200 focus:outline-none focus:ring-0
                   {hasError ? 'border-red-400 focus:border-red-500' : 'border-gray-300 focus:border-indigo-500'}
                   {hasValue || focused ? 'pt-6 pb-2' : 'pt-3 pb-3'}"
            placeholder={label}
        />

        {#if label}
            <label
                for={name}
                class="absolute left-4 text-gray-500 transition-all duration-200 pointer-events-none
                       {hasValue || focused ? 'top-2 text-xs font-medium' : 'top-3 text-base'}
                       {hasError ? 'text-red-500' : (focused ? 'text-indigo-600' : 'text-gray-500')}"
            >
                {label}
            </label>
        {/if}

        <!-- Focus ring -->
        <div
            class="absolute inset-0 rounded-lg pointer-events-none transition-all duration-200
                   {focused ? 'ring-2 ring-indigo-500 ring-opacity-50' : ''}
                   {hasError && focused ? 'ring-red-500' : ''}"
        ></div>
    </div>

    {#if hasError}
        <div class="mt-2 text-sm text-red-600 flex items-center">
            <svg class="w-4 h-4 mr-1 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7 4a1 1 0 11-2 0 1 1 0 012 0zm-1-9a1 1 0 00-1 1v4a1 1 0 102 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
            </svg>
            {errors[0]}
        </div>
    {/if}
</div>

<style>
.input-group {
    margin-bottom: 0;
}
</style>
