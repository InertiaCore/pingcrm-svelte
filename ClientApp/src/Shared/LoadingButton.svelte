<script>
    export let loading = false;
    export let className = '';
    export let variant = 'primary';

    $: props = (({loading, className, variant, ...rest}) => rest)($$props);

    $: buttonClasses = `
        relative flex items-center justify-center px-6 py-3 font-medium text-sm rounded-lg
        transition-all duration-200 transform
        focus:outline-none focus:ring-2 focus:ring-offset-2
        disabled:cursor-not-allowed
        ${loading ? 'cursor-wait' : 'hover:scale-105 active:scale-95'}
        ${variant === 'primary' ?
            `bg-gradient-to-r from-indigo-600 to-indigo-700 hover:from-indigo-700 hover:to-indigo-800
             text-white shadow-lg hover:shadow-xl focus:ring-indigo-500
             ${loading ? 'opacity-90' : ''}` :
            `bg-gray-200 hover:bg-gray-300 text-gray-800 focus:ring-gray-400`}
        ${className}
    `;
</script>

<button
    disabled={loading}
    class={buttonClasses}
    {...props}
>
    {#if loading}
        <div class="absolute inset-0 flex items-center justify-center">
            <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>
        </div>
        <span class="opacity-0">
            <slot/>
        </span>
    {:else}
        <slot/>
    {/if}
</button>
