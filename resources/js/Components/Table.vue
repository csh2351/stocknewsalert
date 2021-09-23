<template>
    <div class="mt-8">
        <h4 class="text-gray-600">Wide Table</h4>
        <div class="flex flex-col mt-6">
            <div
                class="py-2 -my-2 overflow-x-auto sm:-mx-6 sm:px-6 lg:-mx-8 lg:px-8">
                <div
                    class="inline-block min-w-full overflow-hidden align-middle border-b border-gray-200 shadow sm:rounded-lg">
                    <table class="min-w-full">
                        <thead>
                        <tr>
                            <th
                                class="px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                제목 일치
                            </th>
                            <th
                                class="px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                제목 제외
                            </th>
                            <th
                                class="px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                내용 일치
                            </th>
                            <th
                                class="px-6 py-3 text-xs font-medium leading-4 tracking-wider text-left text-gray-500 uppercase bg-gray-100 border-b border-gray-200">
                                내용 제외
                            </th>
                            <th
                                class="px-6 py-3 bg-gray-100 border-b border-gray-200">
                                타입
                            </th>
                            <th
                                class="px-6 py-3 bg-gray-100 border-b border-gray-200">
                                수정
                            </th>
                            <th
                                class="px-6 py-3 bg-gray-100 border-b border-gray-200">
                                삭제
                            </th>
                        </tr>
                        </thead>

                        <tbody class="bg-white">
                        <tr :key="index" v-for="(u, index) in wideTableData">
                            <td
                                class="px-6 py-4 border-b border-gray-200 whitespace-nowrap"
                            >
                                <div class="flex items-center">
                                    <div class="flex-shrink-0 w-10 h-10">
                                        <img
                                            alt="profile pic"
                                            class="w-10 h-10 rounded-full"
                                            src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                                        />
                                    </div>

                                    <div class="ml-4">
                                        <div
                                            class="text-sm font-medium leading-5 text-gray-900"
                                        >
                                            {{ u.name }}
                                        </div>
                                        <div class="text-sm leading-5 text-gray-500">
                                            {{ u.email }}
                                        </div>
                                    </div>
                                </div>
                            </td>

                            <td
                                class="px-6 py-4 border-b border-gray-200 whitespace-nowrap">
                                <div class="text-sm leading-5 text-gray-900">
                                    {{ u.title }}
                                </div>
                                <div class="text-sm leading-5 text-gray-500">
                                    {{ u.title2 }}
                                </div>
                            </td>

                            <td
                                class="px-6 py-4 border-b border-gray-200 whitespace-nowrap">
                    <span
                        class="inline-flex px-2 text-xs font-semibold leading-5 text-green-800 bg-green-100 rounded-full"
                    >{{ u.status }}</span
                    >
                            </td>

                            <td
                                class="px-6 py-4 text-sm leading-5 text-gray-500 border-b border-gray-200 whitespace-nowrap"
                            >
                                {{ u.role }}
                            </td>

                            <td
                                class="px-6 py-4 text-sm font-medium leading-5 text-right border-b border-gray-200 whitespace-nowrap"
                            >
                                <a class="text-indigo-600 hover:text-indigo-900" href="#"
                                >Edit</a
                                >
                            </td>
                        </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            columns: [],
            items: []
        }
    }
</script>
