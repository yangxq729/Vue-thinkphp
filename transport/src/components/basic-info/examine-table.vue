<template>
<div>
    <el-table :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)" stripe style="width:100%" class="select-form">
        <el-table-column prop="checkCode" label="审核流编码"></el-table-column>
        <el-table-column prop="checkName" label="审核名称" ></el-table-column>
        <el-table-column prop="status" label="状态" :filters="[{text:'启用中',value:'启用中'},{text:'停用中',value:'停用中'}]"
          :filter-method="filterstatus" filter-placement="bottom-end">
             <template slot-scope="scope">
                 <i :class="scope.row.status==='启用中'?'el-icon-success':'el-icon-error'" disable-transitions></i>{{scope.row.status}}
             </template>
        </el-table-column>
        <el-table-column prop="remark" label="备注" ></el-table-column>
        <el-table-column label="操作">
            <template slot-scope="scope">
                <el-button size="mini" type="primary" @click="handleStop(scope.$index, scope.row)">停用</el-button>
                <el-button size="mini" type="primary" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
            </template>
        </el-table-column>
    </el-table>
    <el-pagination class="pagination" layout="prev,pager,next" @current-change="current_change"
        :current-page="currentPage"
        :page-size="pageSize" :total="total" background></el-pagination>
</div>
</template>

<script>
export default {
    props:['tableData','total'],
    methods:{
        filterstatus(value, row, column) {
            const property = column['property'];
            return row[property] === value;
        },
    },
    data(){
        return{
            pageSize:3,
            currentPage:1
        }
    },
    methods:{
        current_change(currentPage){
            this.currentPage=currentPage
        }
    }
}
</script>

<style lang="less">
    .btn-form{
        left:7%;position: absolute; top:280px;width: 100%;
        .select-btns-left{
            top:0px;position: absolute;width: 400px;
        }
        .select-btns-right{
            top: 0px;position: absolute;width: 400px;left: 55%;
        }
        .select-form{
            top:50px;position: absolute;
        }
        .pagination{
            top:400px;position: absolute;left: 60%;
        }
    }
</style>
