
import { threadId } from 'worker_threads';
<template>      
    <div>
        <div v-bind:class = "[test.parent]" 
        ref="caseTag" 
        class="container" 
        @click="startEditTestCase(test)"
        v-for="(test, index) in testCaseList" :key="index">

            <div >{{test.caseStep}}</div>

            <div v-bind:class="{parent: test.parent}" v-if=!test.edit>{{test.content}}</div>

            <textarea 
            v-bind:class="{parent: test.parent}"
            v-bind:id="'case_id_'+test.id" 
            ref="text" 
            v-focus 
            v-else 
            @keyup.enter='addTestCase()'
            @keydown.shift.tab.prevent.exact='tabPress()'
            @keydown.tab.prevent.exact='onlyTab()'
            v-model="test.content" 
            autofocus
            ></textarea>
        </div>
    </div>
    
</template>

<script>
export default {
    data: () => ({  
        count:3,
        selectedCaseId: null,
        testCaseInput: null,
        testCaseList: [
        {
            id: 1,
            caseStep: '0001',
            content: "",
            edit: false,
            parent: false,
            child: null
        },
      ]
    }),
    methods:{
        addTestCase: function(){
            this.resetEdit()
            const newIdNumber = this.selectedCaseId + 1
            const newTestCase =  {
                    id: newIdNumber,
                    caseStep: this.setTestCaseNumber(newIdNumber),
                    content: '',
                    edit: true,
                    parent: false,
                    child: null
                }
            this.testCaseList.splice((this.selectedCaseId), 0, newTestCase);
            this.startEditTestCase(newTestCase)
            this.updateTestCaseNumber();
        },
        startEditTestCase: function(test){
            let testIndex = this.testCaseList.findIndex(x => x.id === test.id);
            this.resetEdit()
            this.testCaseList[testIndex].edit = true;
            this.selectedCaseId = testIndex+1;
        },
        setTestCaseNumber: function(testId){
            let num = '0000';
            let numCaseTest = '' + testId
            let idNumber = num.substring(numCaseTest.length) + testId;
            return idNumber;
        },
        resetEdit: function(){
            this.testCaseList.forEach(x => x.edit = false)
        },
        updateTestCaseNumber: function(){

            const whereStartCutitng = this.selectedCaseId;
            let updatedPartTestCaseList = this.testCaseList.slice(whereStartCutitng);
            updatedPartTestCaseList.forEach(test => test.id += 1)
            updatedPartTestCaseList.forEach(test => test.caseStep = this.setTestCaseNumber(test.id))
            const numberOfUpdateObjects = updatedPartTestCaseList.length
            this.testCaseList.slice(whereStartCutitng, numberOfUpdateObjects, updatedPartTestCaseList)
        
        },
        tabPress: function () {
           //it's work now i have to addfunction for this action
           alert('yes')
        },
        onlyTab: function(){
            let testIndex = this.selectedCaseId - 2
            this.testCaseList[testIndex].parent = true
            console.log(this.testCaseList[testIndex])
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
    
    .parent{
        font-size: 30px;
    }
}

</style>

