<template>
    <div>
        <div class="container" v-for="test in testCaseList" :key="test.id">
        <div>{{test.id}}</div>
        <div contenteditable="true ">{{test.content}}</div>
        <div>edit</div>
    </div>
    </div>
    
</template>

<script>
export default {
    data: () => ({
        testCaseList: [
        {
          id: '0001',
          content: "Pierwszy test to jest to"
        },
        {
          id: '0002',
          content: "Drugi test to jest to"
        }
      ]
    })
}
</script>

<style lang="scss" >

.container{
    display:grid;
    grid-template-columns: 40px auto 40px
}

</style>


