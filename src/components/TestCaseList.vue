
<template>

    <div>
        <ul >
            <li class="container" v-for="test in testCaseList" :key="test.id">
                <div>{{test.id}}</div>
                <textarea @keyup.enter='addTestCase()' v-model="test.content"></textarea>
                <div>edit</div>
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
          id: '0001',
          content: "Pierwszy test to jest to",
        },
        {
          id: '0002',
          content: "Drugi test to jest to",
        }
      ]
    }),
    methods:{
        addTestCase: function(){
            this.testCaseList.push(
                {
                    id: '0003',
                    content: '',
                }
            )
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


