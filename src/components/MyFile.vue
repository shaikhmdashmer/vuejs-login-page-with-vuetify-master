<template>
    <div class="myf" id="my-file">
        <table>
            <tr>
                <th>Emp Id</th>
                <th>Name</th>
                <th>Salary</th>
            </tr>
            <tr v-for="e in employee" :key="e.empid">
                <td>{{e.empid}}</td>
                <td v-if="edit_status==e.empid">
                    <input class="eid" type="text" v-model="e.name"/>
                </td>
                <td v-else>{{e.name}}</td>
                <td v-if="edit_status==e.empid">
                    <input class="eid" type="text" v-model="e.salary"/>
                </td>
                <td v-else>{{e.salary}}</td>
                <td v-if="edit_status==e.empid">
                    <button class="btn" @click="editEmployee(e)">Save</button>
                    <button class="btn btnn" @click="edit_status==null">Cancel</button>
                </td>
                <td v-else>
                    <button class="btn" @click="$emit('delete:emp',e.empid);">Delete</button>
                    <button class="btn btnn" @click="edit_details(e.empid)">Edit</button>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
export default {
    name:'my-file',
    props:{
        employee:Array
    },
    data(){
        return{
            edit_status:null
        }
    },
    methods:{
        edit_details(id)
        {
            this.edit_status=id;
        },
        editEmployee(e){
            if(e.name=='' || e.salary=='') return;
            this.$emit('edit:emp',e.empid,e);
            this.edit_status=null;
        }
    },
}
</script>

<style scoped>
table tr th{
padding: 10px;
}
table tr td{
    padding: 10px;
}
.myf{
    display: flex;
    justify-content: center;
}
td{
    text-align:center;
}
.btn{
    background-color:#3f51b5;
    color:white;
    padding:5px 10px;
    border-radius: 5px;
}
.btnn{
    margin-left: 5px;
}
.eid{
    background-color: wheat;
}
</style>