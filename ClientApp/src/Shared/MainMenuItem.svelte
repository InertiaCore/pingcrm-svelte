<script>
    import {Link} from '@inertiajs/svelte';
    import Icon from '@/Shared/Icon.svelte';

    export let icon;
    export let link;
    export let text;

    // Note: Active state detection is now simplified since we removed Ziggy route helper
    // This would need to be updated to use a different method for detecting active routes
    let isActive = false; // Placeholder - implement proper active route detection
</script>

<div class="mb-4">
    <Link href={link} class="flex items-center group py-3">
        <Icon name={icon} className="w-4 h-4 mr-2 {isActive ? 'text-white fill-current' : 'text-indigo-400 group-hover:text-white fill-current'}" />
        <div class={isActive ? 'text-white' : 'text-indigo-200 group-hover:text-white'}>{text}</div>
    </Link>
</div>
