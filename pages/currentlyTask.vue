<template>
  <div class="current-task">
    <h2 class="title">a summary list demo</h2>
    <h3 class="sub-title">2.Current doing in this week</h3>
    <ul class="task-list">
      <li v-for="(item,i) in taskLists" :key="i">
        <Input :class="item.isEdit?'':'no-edit'" clearable v-model="item.remark" :rows="1" maxlength="200"
               :show-word-limit="false" type="textarea" placeholder="Currently doing..." style="width: 200px"/>
        <div class="status">Progress：</div>
        <Input :class="item.isEdit?'':'no-edit'" v-model="item.status" :rows="1" maxlength="2"
               :show-word-limit="false" style="width: 35px;margin-top:10px;"/>
        <Progress :percent="item.status" status="active" />
        <Button type="primary" @click="update(i)" size="small">Update</Button>
        <Button type="primary" @click="save(i)" size="small">Save</Button>
      </li>
    </ul>
    <div class="btn-wrapper">
      <Button type="primary" shape="circle" icon="ios-add-circle-outline" class="add-more-btn" @click="addMore">Add more</Button>
      <a href="/currentlyTask" class="current-doing-btn">To plan <Icon type="ios-arrow-forward" /></a>
    </div>
  </div>
</template>

<script>
    export default {
        name: "currentlyTask",
        data() {
            return {
                newStatus:0,
                taskLists: [
                    {
                        remark: 'currently doing task1',
                        isEdit: false,
                        status:30
                    }, {
                        remark: 'currently doing task2',
                        status:45,
                        isEdit: false
                    }
                ]
            }
        },
        methods:{
            update(i){
                this.taskLists[i].isEdit=true;
            },
            save(i){
                if(this.newStatus>0){
                    this.taskLists[i].status=this.newStatus;
                }
                this.taskLists[i].isEdit=false;
            },
            addMore(){
                let newTask = {
                    remark:'',
                    status:0,
                    isEdit:true
                };
                this.taskLists.push(newTask);
            }
        }
    }
</script>

<style scoped>
  .current-task {
    min-height: 100vh;
    padding: 0 20px;
  }

  .title {
    color: #C41230;
    text-align: center;
    font-size: 30px;
  }

  .sub-title {
    color: #2d8cf0;
    font-size: 18px;
    margin-top: 10px;
  }
  .task-list {
    list-style: none;
  }

  .btn-wrapper{
    padding:20px 0;
    display: flex;
    justify-content: space-around;
  }

  li{
    padding-bottom:10px;
    border-bottom:1px solid #00C58E;
  }
  /deep/ .ivu-btn-small{
    margin:15px 0 5px;
  }
  /deep/ .no-edit .ivu-input {
    border: none;
  }

  /deep/ .no-edit .ivu-input:focus {
    box-shadow: none;
  }

  /deep/ .ivu-input-type-textarea {
    margin-top: 10px;
  }

  .current-doing-btn{
    color: #fff;
    background-color: #2d8cf0;
    display: inline-block;
    margin-bottom: 0;
    font-weight: 400;
    text-align: center;
    vertical-align: middle;
    touch-action: manipulation;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    height: 32px;
    line-height: 29px;
    padding: 0 15px;
    font-size: 14px;
    border-radius: 32px;
    transition: color .2s linear,background-color .2s linear,border .2s linear,box-shadow .2s linear;
  }
</style>
