<template>
    <div id="my-form">
        <form @submit.prevent="submitHandler">
            <table>
                <tr>
                    <td><label>Enter Name: </label></td>
                    <td><input ref="nm" v-model="emp.name" type="text" class="imp" /></td>
                </tr>
                <br>
                <tr>
                    <td><label>Enter Salary: </label></td>
                    <td><input ref="sal" v-model="emp.salary" type="text" id="sal" class="imp"/></td>
                </tr>
            </table>

            <p v-if="error && submit" class="err-msg">
                Please fill all the details!
            </p>
            <p v-if="success" class="success-msg">
                Details added successfully!
            </p>
            <br>
            <div class="btnw"><button class="sbt">ADD PRODUCT</button></div>
        </form>
    </div>
</template>

<script>
export default {
    name:'my-form',
    data(){
        return{
            submit:false,
            error:false,
            success:false,
            emp:{
                name:'',
                salary:''
            }
        }
    },
    computed:{
        invalidName(){
            return this.emp.name==='';
        },
        invalidSalary(){
            return this.emp.salary==='';
        }
    },
    
    methods:{
        submitHandler(){
            this.submit=true;
            if(this.invalidName || this.invalidSalary)
            {
                this.error=true;
                this.success=false;
                if(this.invalidName)
                {
                    
                    this.$refs.nm.classList.add("error_border");
                    
                }
                if(this.invalidSalary)
                {
                    
                    this.$refs.sal.classList.add("error_border");
        
                }
                return;
            }
            this.$emit('add:emp',this.emp);
            
            this.employee={
                name:'',
                salary:''
            }
            this.error=false;
            this.success=true;
            this.submit=false;
            
            //to clear input fields after successful submission
            //to shift focus to first text field after successful submission
            this.emp.name='';
            this.emp.salary='';
            this.$refs.nm.focus();
            
            this.$refs.nm.classList.remove("error_border");
            this.$refs.sal.classList.remove("error_border");
        }
    }
}
</script>

<style scoped>
.err-msg{
    color:red;
    font-weight:bold;
}
.success-msg{
    color:green;
    font-weight:bold;
}
.error_border{
    border:1px solid red;
}
#my-form{
    display: flex;
    justify-content: center;
}
.sbt{
    background-color: #3f51b5;
    color: white;
    padding: 5px 20px ;
    border-radius: 5px;
    
    
}
.btnw{
display: flex;
    justify-content: center;
    margin-bottom: 20px;
}

.imp{
    background-color:wheat;
    margin-left: 10px;
}
</style>