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
                            vaidationFunction: () => {},
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
                            vaidationFunction: () => {},
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
                            vaidationFunction: () => {},
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
                            vaidationFunction: () => {},
                        },
                        {   
                            inputStyle: 'number',
                            name: 'capitalizationPercentage',
                            placeholder: 'Процент капитализации',
                            vaidationFunction: () => {},
                        },
                        {   
                            inputStyle: 'text',
                            placeholder: 'Должность',
                            name: 'position',
                            vaidationFunction: () => {},
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
                                vaidationFunction: () => {},
                            },
                            {   
                                inputStyle: 'text',
                                name: 'productName',
                                placeholder: 'Название продукта',
                                vaidationFunction: () => {},
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
                                vaidationFunction: () => {},
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
                                vaidationFunction: () => {},
                            }
                        ]
                    }
                ],
            },
            submitFunction: () => {
                console.log(123);
            }
        }
    },
}
</script>

<style>

</style>