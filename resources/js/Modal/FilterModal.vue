<template>
    <div aria-labelledby="modal-title" aria-modal="true" class="fixed z-10 inset-0 overflow-y-auto" role="dialog" v-if="show">
        <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <div aria-hidden="true" class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>
            <span aria-hidden="true" class="hidden sm:inline-block sm:align-middle sm:h-screen">&#8203;</span>
            <div
                class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full">
                <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                    <BreezeValidationErrors class="mb-4"/>
                    <form @submit.prevent="submit">
                        <div>
                            <BreezeLabel for="titleMatch" value="제목 포함"/>
                            <BreezeInput autofocus class="mt-1 block w-full" id="titleMatch" type="text"
                                         v-model="form.titleMatchCondition"/>
                        </div>
                        <div class="mt-4">
                            <BreezeLabel for="titleMismatch" value="제목 제외"/>
                            <BreezeInput class="mt-1 block w-full" id="titleMismatch" type="text"
                                         v-model="form.titleUnMatchedCondition"/>
                        </div>
                        <div class="mt-4">
                            <BreezeLabel for="contentsMatch" value="내용 포함"/>
                            <BreezeInput autofocus class="mt-1 block w-full" id="contentsMatch" type="text"
                                         v-model="form.contentsMatchCondition"/>
                        </div>
                        <div class="mt-4">
                            <BreezeLabel for="contentsMismatch" value="내용 제외"/>
                            <BreezeInput class="mt-1 block w-full" id="contentsMismatch" type="text"
                                         v-model="form.contentsUnMatchedCondition"/>
                        </div>
                        <div class="mt-4">
                            <BreezeLabel for="line" value="Line Verify"/>
                            <BreezeInput autocomplete="name" autofocus class="mt-1 block w-full" id="line" required type="text"
                                         v-model="form.lineNotifyId"/>
                        </div>
                        <div class="mt-4">
                            <BreezeDropdown align="left" width="48">
                                <template #trigger>
                                        <span class="inline-flex rounded-md">
                                            <button
                                                class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150"
                                                type="button">
                                                {{ form.type == 0 ? 'News' : 'Reports' }}

                                                <svg class="ml-2 -mr-0.5 h-4 w-4" fill="currentColor" viewBox="0 0 20 20"
                                                     xmlns="http://www.w3.org/2000/svg">
                                                    <path clip-rule="evenodd"
                                                          d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                                          fill-rule="evenodd"/>
                                                </svg>
                                            </button>
                                        </span>
                                </template>
                                <template #content>
                                    <div>
                                        <button
                                            @click="form.type = 0"
                                            class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150"
                                            type="button">
                                            News
                                        </button>
                                    </div>
                                    <div>
                                        <button
                                            @click="form.type = 1"
                                            class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 bg-white hover:text-gray-700 focus:outline-none transition ease-in-out duration-150"
                                            type="button">
                                            Report
                                        </button>
                                    </div>
                                </template>
                            </BreezeDropdown>
                        </div>
                        <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
                            <button
                                class="w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 bg-green-600 text-base font-medium text-white hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500 sm:ml-3 sm:w-auto sm:text-sm"
                                type="submit">
                                등록
                            </button>
                            <button
                                @click="show = false"
                                class="mt-3 w-full inline-flex justify-center rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-base font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm"
                                type="button">
                                취소
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
    import BreezeButton from '@/Components/Button.vue'
    import BreezeInput from '@/Components/Input.vue'
    import BreezeLabel from '@/Components/Label.vue'
    import BreezeDropdown from '@/Components/Dropdown.vue'
    import BreezeValidationErrors from '@/Components/ValidationErrors.vue'
    import Swal from 'sweetalert2'


    export default {
        components: {
            BreezeButton,
            BreezeInput,
            BreezeLabel,
            BreezeDropdown,
            BreezeValidationErrors,
        },

        data() {
            return {
                form: this.$inertia.form({
                    id: '',
                    titleMatchCondition: '',
                    titleUnMatchedCondition: '',
                    contentsMatchCondition: '',
                    contentsUnMatchedCondition: '',
                    lineNotifyId: '',
                    type: 0,
                    userId: 0,
                }),

                show: false,
            }
        },

        methods: {
            submit() {
                if (this.form.id == null) {
                    this.form.post(this.route('filter.store'), {
                        onSuccess: () => {
                            this.form.reset();
                            this.show = false;
                            Swal.fire('추가가 완료되었습니다', '', 'success');
                        },
                        onError: () => {
                            Swal.fire('추가하는 도중 에러가 발생하였습니다.', '', 'error');
                        }
                    });
                } else {
                    this.form.put(this.route('filter.update', this.form), {
                        onSuccess: () => {
                            this.form.reset();
                            this.show = false;
                            Swal.fire('수정이 완료되었습니다', '', 'success');
                        },
                        onError: () => {
                            Swal.fire('수정 도중 도중 에러가 발생하였습니다.', '', 'error');
                        }
                    });
                }

            },
            showModal(filter) {
                this.form.id = filter?.id;
                this.form.titleMatchCondition = filter?.titleMatchCondition;
                this.form.titleUnMatchedCondition = filter?.titleUnMatchedCondition;
                this.form.contentsMatchCondition = filter?.contentsMatchCondition;
                this.form.contentsUnMatchedCondition = filter?.contentsUnMatchedCondition;
                this.form.type = filter == null ? 0 : filter.type;
                this.form.lineNotifyId = filter?.lineNotifyId;
                this.form.userId = this.$page.props.auth.user.id;
                this.show = true;
            }
        }
    }
</script>
