
<template>

    <div>
        <ul >
            <li class="container" v-for="(test, index) in testCaseList" :key="index">
                <div @click="startEditTestCase(test.id)">
                    <div>{{test.id}}</div>
                    <div v-if=!test.edit>{{test.content}}</div>
                    <textarea v-else @keyup.enter='addTestCase()' v-model="test.content"></textarea>
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
        sayHello: function(){
            console.log('hello')},
        addTestCase: function(){
            this.testCaseList.push(
                {
                    id: '0003',
                    content: '',
                }
            )
        },
        startEditTestCase: function(test){
            let testIndex = this.testCaseList.findIndex(x => x.id === test );
            this.testCaseList[testIndex].edit = true;
            console.log(this.testCaseList[testIndex].edit)
        }
    },
}
</script>

<style lang="scss" >

.container{
    display:grid;
    grid-template-columns: 40px auto 40px;
    padding: 0 10px;
}

</style>


