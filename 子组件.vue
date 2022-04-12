<template>
    <div>
        <el-table :data="tableData" style="width: 100%" row-key="id" :header-cell-style="{background: '#f4f3f9', color: '#606266'}"
                  :tree-props="{children: 'children', hasChildren: 'hasChildren'}" @selection-change="handleSelectionChange">
            <template v-for="item in column">
                <el-table-column v-if="item.type" type="selection" :key="Math.random()" :width="item.width" :align="item.align" :reserve-selection="true"></el-table-column>
                <el-table-column v-else :key="item.id" :prop="item.prop" :label="item.label" :width="item.width" :align="item.align" :show-overflow-tooltip="true">
                    <template slot-scope="scope">
                        <ex-slot v-if="item.render" :render="item.render" :row="scope.row" :index="scope.$index" :column="item" />   <!-- column  render函数显示区 -->
                        <span v-else>{{ scope.row[item.prop] || '-' }}</span>                                                        <!-- column  直接绑定的字段显示区 -->
                    </template>
                </el-table-column>
            </template>
        </el-table>
    </div>
</template>

<script>
    let exSlot = {
        functional: true,
        props: {
            row: Object,
            render: Function,
            index: Number,
            column: {
                type: Object,
                default: null
            }
        },
        render: (h, data) => {
            const params = {
                row: data.props.row,
                index: data.props.index
            }
            if (data.props.column) params.column = data.props.column
            return data.props.render(h, params)
        }
    }
    export default {
        name: "Table",
        props: {
            tableData: Array,    // 表格数据
            column: Array,       // 表格显示字段
        },

        methods: {
            handleSelectionChange(val) {
                this.$emit("handleSelectionChange", JSON.stringify(val));
            }
        },

        components: {
            exSlot
        }
    }
</script>

<style scoped>

</style>