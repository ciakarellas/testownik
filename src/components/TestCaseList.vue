
import { nextTick } from 'async';
<template>

    <div>
        <ul >
            <li v-for="(test, index) in testCaseList" :key="index">
                <div ref="caseTag" class="container" @click="startEditTestCase(test.id)">
                    <div>{{test.caseStep}}</div>
                    <div v-if=!test.edit>{{test.content}}</div>
                    <textarea ref="text" v-focus v-else @keyup.enter='addTestCase()' v-model="test.content" autofocus></textarea>
                    <div>edit</div>
                </div>
            </li>
        </ul>
    </div>
    
</template>

<script>
export default {
    data: () => ({  
        testCaseInput: null,
        testCaseList: [
        {
            id: 1,
            caseStep: '0001',
            content: "Pierwszy test to jest to",
            edit: false
        },
        {
            id: 2,
            caseStep: '0002',
            content: "Drugi test to jest to",
            edit: false
        }
      ]
    }),
    methods:{
        addTestCase: function(){
            this.resetEdit()
            this.testCaseList.push(
                {
                    id: this.testCaseList.length + 1,
                    caseStep: this.setTestCaseNumber(),
                    content: '',
                    edit: true
                }
            );
        },
        startEditTestCase: function(test){
            let testIndex = this.testCaseList.findIndex(x => x.id === test );
            this.resetEdit()
            this.testCaseList[testIndex].edit = true;
        },
        setTestCaseNumber: function(){
            let num = '0000';
            let numCaseTest = '' + (this.testCaseList.length + 1)
            let idNumber = num.substring(   numCaseTest.length) + (this.testCaseList.length + 1);
            return idNumber;
        },
        resetEdit: function(){
            this.testCaseList.forEach(x => x.edit = false)
        }
    },
    directives: {
        focus: {
            // directive definition
            inserted: function (el) {
            el.focus()
            }
        }
    }
}
</script>

<style lang="scss" >

.container{
    display:grid;
    grid-template-columns: 40px auto 40px;
    padding: 0 10px;
    width:80%;
}

</style>


