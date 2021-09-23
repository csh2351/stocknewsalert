<template>
    <Head title="Filter"/>

    <BreezeAuthenticatedLayout>
        <template #header>
            <div class="flex">
                <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                    Filter List
                </h2>
                <button
                    @click="showFilterModal"
                    class="inline-flex text-sm font-semibold leading-5 text-blue-800 bg-blue-100 hover:bg-blue-500 rounded-full ml-auto items-center">
                    <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path d="M12 9v3m0 0v3m0-3h3m-3 0H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" stroke-linecap="round" stroke-linejoin="round"
                              stroke-width="2"/>
                    </svg>
                    Add Filter
                </button>
            </div>
        </template>
        <div class="py-8 text-center">
            <div class="mx-auto sm:px-6 lg:px-8 text-center" style="text-align: -webkit-center">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg max-w-max">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <div class="py-2 -my-2 overflow-x-auto sm:-mx-6 sm:px-6 lg:-mx-8 lg:px-8">
                            <div class="inline-block overflow-hidden align-middle border-b border-gray-200 shadow sm:rounded-lg">
                                <table class="table-fixed">
                                    <thead>
                                    <tr>
                                        <th class="px-6 py-3 text-sm font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                            제목 일치
                                        </th>
                                        <th class="px-6 py-3 text-sm font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                            제목 제외
                                        </th>
                                        <th class="px-6 py-3 text-sm font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                            내용 일치
                                        </th>
                                        <th class="px-6 py-3 text-sm font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                            내용 제외
                                        </th>
                                        <th class="px-6 py-3 text-sm font-medium leading-4 tracking-wider text-center text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                            타입
                                        </th>
                                        <th class="px-2 py-3 text-sm font-medium leading-4 tracking-wider text-center text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                        </th>
                                        <th class="px-2 py-3 text-sm font-medium leading-4 tracking-wider text-center text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                        </th>
                                    </tr>
                                    </thead>

                                    <tbody class="bg-white">
                                    <tr :key="index" v-for="(item, index) in items">
                                        <td class="px-6 py-4 border-b border-gray-200 whitespace-nowrap">
                                            <div :title="item.titleMatchCondition"
                                                 class="text-sm leading-5 text-gray-500 max-w-xs overflow-hidden overflow-ellipsis">
                                                {{item.titleMatchCondition }}
                                            </div>
                                        </td>

                                        <td class="px-6 py-4 border-b border-gray-200 whitespace-nowrap">
                                            <div :title="item.titleUnMatchedCondition"
                                                 class="text-sm leading-5 text-gray-500 max-w-xs overflow-hidden overflow-ellipsis">
                                                {{item.titleUnMatchedCondition }}
                                            </div>
                                        </td>

                                        <td class="px-6 py-4 border-b border-gray-200 whitespace-nowrap">
                                            <div :title="item.contentsMatchCondition"
                                                 class="text-sm leading-5 text-gray-500 max-w-xs overflow-hidden overflow-ellipsis">
                                                {{item.contentsMatchCondition }}
                                            </div>
                                        </td>

                                        <td class="px-6 py-4 border-b border-gray-200 whitespace-nowrap">
                                            <div :title="item.contentsUnMatchedCondition"
                                                 class="text-sm leading-5 text-gray-500 max-w-xs overflow-hidden overflow-ellipsis">
                                                {{item.contentsUnMatchedCondition }}
                                            </div>
                                        </td>

                                        <td class="px-6 py-4 text-sm font-medium leading-5 text-center border-b border-gray-200 whitespace-nowrap">
                                            {{ item.type == 1 ? "Report" : "News"}}
                                        </td>

                                        <td class="px-4 py-4 text-sm font-medium leading-5 text-center border-b border-gray-200 whitespace-nowrap">
                                            <button
                                                @click="showFilterModal(item)"
                                                class="inline-flex text-sm font-semibold leading-5 text-green-800 bg-green-100 hover:bg-green-500 rounded-full">
                                                <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"
                                                     xmlns="http://www.w3.org/2000/svg">
                                                    <path
                                                        d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
                                                        stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"/>
                                                </svg>
                                            </button>
                                        </td>
                                        <td class="px-4 py-4 text-sm font-medium leading-5 text-center border-b border-gray-200 whitespace-nowrap">
                                            <button
                                                @click="deleteFilter(item.id)"
                                                class="inline-flex text-sm font-semibold leading-5 text-red-800 bg-red-100 hover:bg-red-500 rounded-full">
                                                <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"
                                                     xmlns="http://www.w3.org/2000/svg">
                                                    <path
                                                        d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                                                        stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"/>
                                                </svg>
                                            </button>
                                        </td>
                                    </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <filter-modal ref="filterModal"/>
    </BreezeAuthenticatedLayout>
</template>

<script>
    import BreezeAuthenticatedLayout from '@/Layouts/Authenticated.vue'
    import {Head} from '@inertiajs/inertia-vue3';
    import Button from "../Components/Button";
    import Swal from 'sweetalert2'
    import FilterModal from "@/Modal/FilterModal";

    export default {
        components: {
            Button,
            BreezeAuthenticatedLayout,
            FilterModal,
            Head,
        },
        props: {
            items: Array,
        },
        methods: {
            deleteFilter(item) {
                Swal.fire({
                    title: '삭제하시겠습니까?',
                    showDenyButton: true,
                    confirmButtonText: 'Yes',
                    denyButtonText: 'No',
                    customClass: {
                        actions: 'my-actions',
                        confirmButton: 'order-2',
                        denyButton: 'order-3',
                    }
                }).then((result) => {
                    if (result.isConfirmed) {
                        this.$inertia.delete(this.route('filter.destroy', {
                            filter: item,
                        })).then((response) => {
                            if (response.status == 200) {
                                Swal.fire('삭제되었습니다', '', 'success');
                            }
                        });
                    }
                })
            },
            showFilterModal(filter){
                this.$refs.filterModal.showModal(filter);
            }
        }
    }
</script>
