<template>
    <div>
        <form-component-vue :componentProps=this.componentProps />
    </div>
</template>

<script>

import managerAvavtar from '@/assets/images/avatar.png'
import selectUserIcon from '@/assets/icons/avatar.svg'
import FormComponentVue from '@/components/FormComponent.vue';
export default {
    components: {
        FormComponentVue,
    },
    data() {
        return {
            componentProps: {
                title: 'создание',
                subtitle: 'Данные',
                modalData: {
                    title: 'Создать сотрудника',
                    inputs: [
                        {   
                            inputStyle: 'select-employ',
                            avatar: selectUserIcon,
                            name: 'employee',
                            placeholder: 'Сотрудник',
                            event: 'pressed',
                            options: [
                                {
                                    text: 'Инван Иванов',
                                    value: 1,
                                    imgSrc: managerAvavtar,
                                },
                                {
                                    text: 'Инван Иванов',
                                    value: 2,
                                    imgSrc: '',
                                },
                            ],
                        },
                        {   
                            inputStyle: 'select-employ',
                            avatar: selectUserIcon,
                            name: 'boss',
                            placeholder: 'Руководитель',
                            event: 'pressed',
                            options: [
                                {
                                    text: 'Инван Иванов',
                                    value: 1,
                                    imgSrc: managerAvavtar,
                                },
                                {
                                    text: 'Инван Иванов',
                                    value: 2,
                                    imgSrc: '',
                                },
                            ],
                        },
                        {   
                            inputStyle: 'select',
                            placeholder: 'Тип ставки',
                            name: 'bet',
                            options: [
                                {
                                    text: 'opex',
                                    value: 1,
                                },
                                {
                                    text: 'capex',
                                    value: 2,
                                },
                            ],
                        },
                        {   
                            inputStyle: 'select',
                            placeholder: 'Бизнес-единица',
                            name: 'buisnessUnit',
                            options: [
                                {
                                    text: 'MVM',
                                    value: 1,
                                },
                                {
                                    text: 'MTech',
                                    value: 2,
                                },
                            ],
                        },
                        {   
                            inputStyle: 'number',
                            name: 'capitalizationPercentage',
                            placeholder: 'Процент капитализации',
                        },
                        {   
                            inputStyle: 'text',
                            placeholder: 'Должность',
                            name: 'position',
                        },
                    ]
                },
                inputBlocks: [
                    {   
                        inputs: [
                            {   
                                inputStyle: 'select-employ',
                                avatar: selectUserIcon,
                                placeholder: 'Менеджер',
                                name: 'manager',
                                event: 'openModal',
                                options: [
                                    {
                                        text: 'Инван Иванов',
                                        value: 1,
                                        imgSrc: managerAvavtar,
                                    },
                                    {
                                        text: 'Инван Иванов',
                                        value: 2,
                                        imgSrc: '',
                                    },
                                ],
                            },
                            {   
                                inputStyle: 'text',
                                name: 'productName',
                                placeholder: 'Название продукта',
                            },
                        ]
                    },
                    {
                        inputs: [
                            {   
                                inputStyle: 'text',
                                name: 'url',
                                label: 'Ссылка в jira, вкючая https://',
                                placeholder: 'Название продукта',
                            },
                            {   
                                inputStyle: 'select',
                                name: 'domain',
                                placeholder: 'Домен',
                                options: [
                                    {
                                        text: 'Бэк-офис',
                                        value: 1,
                                    },
                                    {
                                        text: 'Техплатформа',
                                        value: 2,
                                    },
                                    {
                                        text: 'Офис больших данных',
                                        value: 3,
                                    },
                                    {
                                        text: 'Цифровой опыт поставщика',
                                        value: 4,
                                    },
                                ],
                            }
                        ]
                    }
                ],
            },
        }
    },
}
</script>

<style>

</style>