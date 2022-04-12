<template>
    <div>
        test
        <Table :tableData="tableData" :column="column"></Table>
    </div>
</template>

<script>
    import Table from "./Table"
    export default {
        name: "Test",

        data() {
            return{
                tableData: [
                    {id: '1', user: 'zhangsan1', nick: '张三'},
                    {id: '2', user: 'zhangsan2', nick: '张三'},
                    {id: '3', user: 'zhangsan3', nick: '张三'},
                    {id: '4', user: 'zhangsan4', nick: '张三'},
                    {id: '5', user: 'zhangsan5', nick: '张三', children: [
                        {id: "51", user: '11'}
                    ]},
                ],
                column: [
                    {id: -1, type: 'selection', align: "right", width: 60},
                    {id: 0, label: '序号', align: "center", render: (h, record)=>{
                        return h("span", record.index+1)
                    }},
                    {id: 1, prop: 'user', label: '用户名', align: 'center'},
                    {id: 2, prop: 'nick', label: '昵称', align: 'center', render: (h, record)=>{
                            return h("span", "你猜");
                        }},
                    {id: 3, label: '操作', align: "center", render:(h,params)=>{
                            let arr = []
                            arr.push(h("el-button",{
                                props: {
                                    type:"primary",
                                    icon:"el-icon-edit",
                                    size: 'mini'
                                },
                                on:{
                                    click:()=>{
                                        const index = this.tableData.findIndex(item=>item.id == params.row.id);
                                        this.tableData.splice(index, 1);
                                    }
                                }
                            }, "新增"))
                            arr.push(h("div",{
                                on:{
                                    click:()=>{
                                        console.log(params)
                                    }
                                },
                                style: {
                                    color: "red",
                                    cursor: "pointer",
                                    marginLeft: "20px"
                                },
                                attrs:{
                                    title: "测试",
                                    class: "el-icon-edit"
                                }
                            }))
                            return h('div',arr)
                        }
                    }
                ]
            }
        },

        methods: {

        },

        components: {
            Table
        }
    }
</script>

<style scoped>

</style>