<script>
    import { Link, page } from '@inertiajs/svelte';
    import Helmet from '@/Shared/Helmet.svelte';
    import Layout from '@/Shared/Layout.svelte';
    import Icon from '@/Shared/Icon.svelte';
    import SearchFilter from '@/Shared/SearchFilter.svelte';
    import Pagination from '@/Shared/Pagination.svelte';


    $: data = $page?.users?.data || [];
    $: links = $page?.users?.links || [];
</script>

<Helmet title="Users" />

<Layout>
    <div>
        <h1 class="mb-8 font-bold text-3xl">Users</h1>

        <div class="mb-6 flex justify-between items-center">
            <SearchFilter />

            <Link class="btn-indigo" href="/users/create">
                <span>Create</span>
                <span class="hidden md:inline"> User</span>
            </Link>
        </div>

        <div class="bg-white rounded shadow overflow-x-auto">
            <table class="w-full whitespace-no-wrap">
                <thead>
                    <tr class="text-left font-bold">
                        <th class="px-6 pt-5 pb-4">Name</th>
                        <th class="px-6 pt-5 pb-4">Email</th>
                        <th class="px-6 pt-5 pb-4" colspan="2">Role</th>
                    </tr>
                </thead>
                <tbody>
                    {#if !data || data.length === 0}
                        <tr>
                            <td class="border-t px-6 py-4" colspan="4">
                                No users found.
                            </td>
                        </tr>
                    {:else}
                        {#each data as { id, name, photo, email, owner, deleted_at } (id)}
                            <tr class="hover:bg-gray-100 focus-within:bg-gray-100">
                                <td class="border-t">
                                    <Link
                                        href={`/users/${id}/edit`}
                                        class="px-6 py-4 flex items-center focus:text-indigo-700"
                                    >
                                    {#if photo}
                                        <img
                                            src={photo}
                                            class="block w-5 h-5 rounded-full mr-2 -my-2"
                                            alt={name}
                                        />
                                    {/if}
                                    {name}
                                    {#if deleted_at}
                                        <Icon
                                            name="trash"
                                            className="flex-shrink-0 w-3 h-3 text-gray-400 fill-current ml-2"
                                        />
                                    {/if}
                                    </Link>
                                </td>

                                <td class="border-t">
                                    <Link
                                        tabindex="-1"
                                        href={`/users/${id}/edit`}
                                        class="px-6 py-4 flex items-center focus:text-indigo"
                                    >
                                        {email}
                                    </Link>
                                </td>

                                <td class="border-t">
                                    <Link
                                        tabindex="-1"
                                        href={`/users/${id}/edit`}
                                        class="px-6 py-4 flex items-center focus:text-indigo"
                                    >
                                        {owner ? 'Owner' : 'User'}
                                    </Link>
                                </td>

                                <td class="border-t w-px">
                                    <Link
                                        tabindex="-1"
                                        href={`/users/${id}/edit`}
                                        class="px-4 flex items-center"
                                    >
                                        <Icon
                                            name="cheveron-right"
                                            className="block w-6 h-6 text-gray-400 fill-current"
                                        />
                                    </Link>
                                </td>
                            </tr>
                        {/each}
                    {/if}
                </tbody>
            </table>
        </div>

        <Pagination links={links} />
    </div>
</Layout>
