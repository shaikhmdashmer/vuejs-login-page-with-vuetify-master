<template>
    <div id="my-app">
        <my-form @add:emp="addEmployee"/>
        <my-file v-bind:employee="employee" @delete:emp="delEmployee" @edit:emp="editEmployee"/>
    </div>
</template>

<script>
import MyFile from './components/MyFile.vue'
import MyForm from './components/MyForm.vue'

export default {
    name:'MyApp',
    components:{
        MyFile,
        MyForm,
    },
    data(){
        return{
            employee:[
                {
                    empid:1,
                    name:'John',
                    salary:'8000'
                },
                {
                    empid:2,
                    name:'James',
                    salary:'8200'
                },
                {
                    empid:3,
                    name:'Sam',
                    salary:'8800'
                }
            ]
        }
    },
    methods:{
        addEmployee(emp)
        {
            const lastid=this.employee.length>0?this.employee[this.employee.length-1].empid:0;
            const empid=lastid+1;
            const newEmp={...emp,empid};
            this.employee=[...this.employee,newEmp];
        },
        delEmployee(empid){
            this.employee=this.employee.filter(val=>val.empid!=empid);
        },
        editEmployee(empid,empl){
            this.employee=this.employee.map(val=>
                val.id===empid?empl:val
            )
        }
    }
}
</script>

<style>

</style>